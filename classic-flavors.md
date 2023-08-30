---

copyright: 
  years: 2014, 2023
lastupdated: "2023-08-30"

keywords: openshift, node scaling, ca, autoscaler

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}



# Classic flavors
{: #classic-flavors}

Review the classic worker node flavors by metro.





## `ams`
{: #ams}

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | 
| b3c.16x64 | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.16x64.300gb | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 300GB SSD |
| b3c.32x128 | 32, 128GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.4x16 | 4, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.56x242 | 56, 242GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.8x32 | 8, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.16x16 | 16, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.16x32 | 16, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.32x32 | 32, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.32x64 | 32, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| m3c.4x32 | 4, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| mb4c.20x192 | 20, 192GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.20x384 | 20, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.20x64 | 20, 64GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.20x64.2x1.9tb.ssd | 20, 64GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.32x384.3.8tb.ssd | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 1920GB SSD |
| mb4c.32x384.6x3.8tb.ssd | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 1920GB SSD |
| mb4c.32x768.3.8tb.ssd | 32, 768GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.48x1536 | 48, 1536GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| me4c.4x32 | 4, 32GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 2000GB HDD |
| me4c.4x32.1.9tb.ssd | 4, 32GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mg4c.32x384.2xp100 | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mg4c.48x384.2xv100 | 48, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| u3c.2x4 | 2, 4GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
{: caption="Table 1. Worker node flavors for Amsterdam." caption-side="bottom"}



## `che`
{: #che}

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | 
| b3c.16x64 | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.16x64.300gb | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 300GB SSD |
| b3c.32x128 | 32, 128GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.4x16 | 4, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.56x242 | 56, 242GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.8x32 | 8, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.16x16 | 16, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.16x32 | 16, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.32x32 | 32, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.32x64 | 32, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| m3c.4x32 | 4, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| mb4c.20x192 | 20, 192GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.20x384 | 20, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.20x64 | 20, 64GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.20x64.2x1.9tb.ssd | 20, 64GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.32x384.3.8tb.ssd | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 1920GB SSD |
| mb4c.32x384.6x3.8tb.ssd | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 1920GB SSD |
| mb4c.32x768.3.8tb.ssd | 32, 768GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.48x1536 | 48, 1536GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| me4c.4x32 | 4, 32GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 2000GB HDD |
| me4c.4x32.1.9tb.ssd | 4, 32GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mg4c.32x384.2xp100 | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mg4c.48x384.2xv100 | 48, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| u3c.2x4 | 2, 4GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
{: caption="Table 2. Worker node flavors for Chennai." caption-side="bottom"}



## `dal`
{: #dal}

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | 
| b3c.16x64 | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.16x64.300gb | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 300GB SSD |
| b3c.32x128 | 32, 128GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.4x16 | 4, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.56x242 | 56, 242GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.8x32 | 8, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.16x16 | 16, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.16x32 | 16, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.32x32 | 32, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.32x64 | 32, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| m3c.16x128 | 16, 128GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| m3c.30x240 | 30, 240GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| m3c.48x384 | 48, 384GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| m3c.4x32 | 4, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| m3c.56x448 | 56, 448GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| m3c.64x512 | 64, 512GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| m3c.8x64 | 8, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| mb4c.20x192 | 20, 192GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.20x384 | 20, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.20x64 | 20, 64GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.20x64.2x1.9tb.ssd | 20, 64GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.32x384.3.8tb.ssd | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 1920GB SSD |
| mb4c.32x384.6x3.8tb.ssd | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 1920GB SSD |
| mb4c.32x768.3.8tb.ssd | 32, 768GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.48x1536 | 48, 1536GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| me4c.4x32 | 4, 32GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 2000GB HDD |
| me4c.4x32.1.9tb.ssd | 4, 32GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mg4c.32x384.2xp100 | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mg4c.48x384.2xv100 | 48, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| u3c.2x4 | 2, 4GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
{: caption="Table 3. Worker node flavors for Dallas." caption-side="bottom"}



## `fra`
{: #fra}

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | 
| b3c.16x64 | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.16x64.300gb | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 300GB SSD |
| b3c.32x128 | 32, 128GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.4x16 | 4, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.56x242 | 56, 242GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.8x32 | 8, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.16x16 | 16, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.16x32 | 16, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.32x32 | 32, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.32x64 | 32, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| m3c.16x128 | 16, 128GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| m3c.30x240 | 30, 240GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| m3c.4x32 | 4, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| m3c.8x64 | 8, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| mb4c.20x192 | 20, 192GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.20x384 | 20, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.20x64 | 20, 64GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.20x64.2x1.9tb.ssd | 20, 64GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.32x384.3.8tb.ssd | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 1920GB SSD |
| mb4c.32x384.6x3.8tb.ssd | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 1920GB SSD |
| mb4c.32x768.3.8tb.ssd | 32, 768GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.48x1536 | 48, 1536GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| me4c.4x32 | 4, 32GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 2000GB HDD |
| me4c.4x32.1.9tb.ssd | 4, 32GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mg4c.32x384.2xp100 | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mg4c.48x384.2xv100 | 48, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| u3c.2x4 | 2, 4GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
{: caption="Table 4. Worker node flavors for France." caption-side="bottom"}



## `lon`
{: #lon}

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | 
| b3c.16x64 | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.16x64.300gb | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 300GB SSD |
| b3c.32x128 | 32, 128GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.4x16 | 4, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.56x242 | 56, 242GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.8x32 | 8, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.16x16 | 16, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.16x32 | 16, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.32x32 | 32, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.32x64 | 32, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| m3c.16x128 | 16, 128GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| m3c.30x240 | 30, 240GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| m3c.4x32 | 4, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| m3c.8x64 | 8, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| mb4c.20x192 | 20, 192GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.20x384 | 20, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.20x64 | 20, 64GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.20x64.2x1.9tb.ssd | 20, 64GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.32x384.3.8tb.ssd | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 1920GB SSD |
| mb4c.32x384.6x3.8tb.ssd | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 1920GB SSD |
| mb4c.32x768.3.8tb.ssd | 32, 768GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.48x1536 | 48, 1536GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| me4c.4x32 | 4, 32GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 2000GB HDD |
| me4c.4x32.1.9tb.ssd | 4, 32GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mg4c.32x384.2xp100 | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mg4c.48x384.2xv100 | 48, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| u3c.2x4 | 2, 4GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
{: caption="Table 5. Worker node flavors for London." caption-side="bottom"}



## `mil`
{: #mil}

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | 
| b3c.16x64 | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.16x64.300gb | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 300GB SSD |
| b3c.32x128 | 32, 128GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.4x16 | 4, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.56x242 | 56, 242GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.8x32 | 8, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.16x16 | 16, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.16x32 | 16, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.32x32 | 32, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.32x64 | 32, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| m3c.4x32 | 4, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| mb4c.20x192 | 20, 192GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.20x384 | 20, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.20x64 | 20, 64GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.20x64.2x1.9tb.ssd | 20, 64GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.32x384.3.8tb.ssd | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 1920GB SSD |
| mb4c.32x384.6x3.8tb.ssd | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 1920GB SSD |
| mb4c.32x768.3.8tb.ssd | 32, 768GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.48x1536 | 48, 1536GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| me4c.4x32 | 4, 32GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 2000GB HDD |
| me4c.4x32.1.9tb.ssd | 4, 32GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mg4c.32x384.2xp100 | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mg4c.48x384.2xv100 | 48, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| u3c.2x4 | 2, 4GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
{: caption="Table 6. Worker node flavors for Milan." caption-side="bottom"}



## `mon`
{: #mon}

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | 
| b3c.16x64 | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.16x64.300gb | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 300GB SSD |
| b3c.32x128 | 32, 128GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.4x16 | 4, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.56x242 | 56, 242GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.8x32 | 8, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.16x16 | 16, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.16x32 | 16, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.32x32 | 32, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.32x64 | 32, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| m3c.4x32 | 4, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| mb4c.20x192 | 20, 192GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.20x384 | 20, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.20x64 | 20, 64GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.20x64.2x1.9tb.ssd | 20, 64GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.32x384.3.8tb.ssd | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 1920GB SSD |
| mb4c.32x384.6x3.8tb.ssd | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 1920GB SSD |
| mb4c.32x768.3.8tb.ssd | 32, 768GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.48x1536 | 48, 1536GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| me4c.4x32 | 4, 32GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 2000GB HDD |
| me4c.4x32.1.9tb.ssd | 4, 32GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mg4c.32x384.2xp100 | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mg4c.48x384.2xv100 | 48, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| u3c.2x4 | 2, 4GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
{: caption="Table 7. Worker node flavors for Montreal." caption-side="bottom"}



## `osa`
{: #osa}

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | 
| b3c.16x64 | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.16x64.300gb | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 300GB SSD |
| b3c.32x128 | 32, 128GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.4x16 | 4, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.56x242 | 56, 242GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.8x32 | 8, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.16x16 | 16, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.16x32 | 16, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.32x32 | 32, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.32x64 | 32, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| m3c.16x128 | 16, 128GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| m3c.30x240 | 30, 240GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| m3c.48x384 | 48, 384GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| m3c.4x32 | 4, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| m3c.56x448 | 56, 448GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| m3c.64x512 | 64, 512GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| m3c.8x64 | 8, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| mb4c.20x192 | 20, 192GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.20x384 | 20, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.20x64 | 20, 64GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.20x64.2x1.9tb.ssd | 20, 64GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.32x384.3.8tb.ssd | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 1920GB SSD |
| mb4c.32x384.6x3.8tb.ssd | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 1920GB SSD |
| mb4c.32x768.3.8tb.ssd | 32, 768GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.48x1536 | 48, 1536GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| me4c.4x32 | 4, 32GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 2000GB HDD |
| me4c.4x32.1.9tb.ssd | 4, 32GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mg4c.32x384.2xp100 | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mg4c.48x384.2xv100 | 48, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| u3c.2x4 | 2, 4GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
{: caption="Table 8. Worker node flavors for Osaka." caption-side="bottom"}



## `par`
{: #par}

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | 
| b3c.16x64 | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.16x64.300gb | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 300GB SSD |
| b3c.32x128 | 32, 128GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.4x16 | 4, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.56x242 | 56, 242GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.8x32 | 8, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.16x16 | 16, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.16x32 | 16, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.32x32 | 32, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.32x64 | 32, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| m3c.16x128 | 16, 128GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| m3c.30x240 | 30, 240GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| m3c.4x32 | 4, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| m3c.8x64 | 8, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| mb4c.20x192 | 20, 192GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.20x384 | 20, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.20x64 | 20, 64GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.20x64.2x1.9tb.ssd | 20, 64GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.32x384.3.8tb.ssd | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 1920GB SSD |
| mb4c.32x384.6x3.8tb.ssd | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 1920GB SSD |
| mb4c.32x768.3.8tb.ssd | 32, 768GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.48x1536 | 48, 1536GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| me4c.4x32 | 4, 32GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 2000GB HDD |
| me4c.4x32.1.9tb.ssd | 4, 32GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mg4c.32x384.2xp100 | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mg4c.48x384.2xv100 | 48, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| u3c.2x4 | 2, 4GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
{: caption="Table 9. Worker node flavors for Paris." caption-side="bottom"}



## `sao`
{: #sao}

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | 
| b3c.16x64 | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.16x64.300gb | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 300GB SSD |
| b3c.32x128 | 32, 128GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.4x16 | 4, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.56x242 | 56, 242GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.8x32 | 8, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| m3c.4x32 | 4, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| u3c.2x4 | 2, 4GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
{: caption="Table 10. Worker node flavors for South America." caption-side="bottom"}



## `sjc`
{: #sjc}

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | 
| b3c.16x64 | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.16x64.300gb | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 300GB SSD |
| b3c.32x128 | 32, 128GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.4x16 | 4, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.56x242 | 56, 242GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.8x32 | 8, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.16x16 | 16, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.16x32 | 16, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.32x32 | 32, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.32x64 | 32, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| m3c.4x32 | 4, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| u3c.2x4 | 2, 4GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
{: caption="Table 11. Worker node flavors for San Jose." caption-side="bottom"}



## `sng`
{: #sng}

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | 
| b3c.16x64 | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.16x64.300gb | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 300GB SSD |
| b3c.4x16 | 4, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.8x32 | 8, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.16x16 | 16, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.16x32 | 16, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| m3c.4x32 | 4, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| u3c.2x4 | 2, 4GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
{: caption="Table 12. Worker node flavors for Singapore." caption-side="bottom"}



## `syd`
{: #syd}

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | 
| b3c.16x64 | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.16x64.300gb | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 300GB SSD |
| b3c.32x128 | 32, 128GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.4x16 | 4, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.56x242 | 56, 242GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.8x32 | 8, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.16x16 | 16, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.16x32 | 16, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.32x32 | 32, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.32x64 | 32, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| m3c.16x128 | 16, 128GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| m3c.30x240 | 30, 240GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| m3c.4x32 | 4, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| m3c.8x64 | 8, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| mb4c.20x192 | 20, 192GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.20x384 | 20, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.20x64 | 20, 64GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.20x64.2x1.9tb.ssd | 20, 64GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.32x384.3.8tb.ssd | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 1920GB SSD |
| mb4c.32x384.6x3.8tb.ssd | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 1920GB SSD |
| mb4c.32x768.3.8tb.ssd | 32, 768GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.48x1536 | 48, 1536GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| me4c.4x32 | 4, 32GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 2000GB HDD |
| me4c.4x32.1.9tb.ssd | 4, 32GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mg4c.32x384.2xp100 | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mg4c.48x384.2xv100 | 48, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| u3c.2x4 | 2, 4GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
{: caption="Table 13. Worker node flavors for Sydney." caption-side="bottom"}



## `tok`
{: #tok}

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | 
| b3c.16x64 | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.16x64.300gb | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 300GB SSD |
| b3c.32x128 | 32, 128GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.4x16 | 4, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.56x242 | 56, 242GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.8x32 | 8, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.16x16 | 16, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.16x32 | 16, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.32x32 | 32, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.32x64 | 32, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| m3c.16x128 | 16, 128GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| m3c.30x240 | 30, 240GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| m3c.4x32 | 4, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| m3c.8x64 | 8, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| mb4c.20x192 | 20, 192GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.20x384 | 20, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.20x64 | 20, 64GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.20x64.2x1.9tb.ssd | 20, 64GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.32x384.3.8tb.ssd | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 1920GB SSD |
| mb4c.32x384.6x3.8tb.ssd | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 1920GB SSD |
| mb4c.32x768.3.8tb.ssd | 32, 768GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.48x1536 | 48, 1536GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| me4c.4x32 | 4, 32GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 2000GB HDD |
| me4c.4x32.1.9tb.ssd | 4, 32GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mg4c.32x384.2xp100 | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mg4c.48x384.2xv100 | 48, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| u3c.2x4 | 2, 4GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
{: caption="Table 14. Worker node flavors for Tokyo." caption-side="bottom"}



## `tor`
{: #tor}

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | 
| b3c.16x64 | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.16x64.300gb | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 300GB SSD |
| b3c.32x128 | 32, 128GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.4x16 | 4, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.56x242 | 56, 242GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.8x32 | 8, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.16x16 | 16, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.16x32 | 16, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.32x32 | 32, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.32x64 | 32, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| m3c.16x128 | 16, 128GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| m3c.30x240 | 30, 240GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| m3c.4x32 | 4, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| m3c.8x64 | 8, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| mb4c.20x192 | 20, 192GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.20x384 | 20, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.20x64 | 20, 64GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.20x64.2x1.9tb.ssd | 20, 64GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.32x384.3.8tb.ssd | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 1920GB SSD |
| mb4c.32x384.6x3.8tb.ssd | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 1920GB SSD |
| mb4c.32x768.3.8tb.ssd | 32, 768GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.48x1536 | 48, 1536GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| me4c.4x32 | 4, 32GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 2000GB HDD |
| me4c.4x32.1.9tb.ssd | 4, 32GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mg4c.32x384.2xp100 | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mg4c.48x384.2xv100 | 48, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| u3c.2x4 | 2, 4GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
{: caption="Table 15. Worker node flavors for Toronto." caption-side="bottom"}



## `wdc`
{: #wdc}

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | 
| b3c.16x64 | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.16x64.300gb | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 300GB SSD |
| b3c.32x128 | 32, 128GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.4x16 | 4, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.56x242 | 56, 242GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| b3c.8x32 | 8, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.16x16 | 16, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.16x32 | 16, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.32x32 | 32, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| c3c.32x64 | 32, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| m3c.16x128 | 16, 128GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| m3c.30x240 | 30, 240GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| m3c.4x32 | 4, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| m3c.8x64 | 8, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
| mb4c.20x192 | 20, 192GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.20x384 | 20, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.20x64 | 20, 64GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.20x64.2x1.9tb.ssd | 20, 64GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.32x384.3.8tb.ssd | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 1920GB SSD |
| mb4c.32x384.6x3.8tb.ssd | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 1920GB SSD |
| mb4c.32x768.3.8tb.ssd | 32, 768GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mb4c.48x1536 | 48, 1536GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| me4c.4x32 | 4, 32GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 2000GB HDD |
| me4c.4x32.1.9tb.ssd | 4, 32GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mg4c.32x384.2xp100 | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| mg4c.48x384.2xv100 | 48, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |
| u3c.2x4 | 2, 4GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD |
{: caption="Table 16. Worker node flavors for Washington DC." caption-side="bottom"}






