---

copyright: 
  years: 2014, 2023
lastupdated: "2023-10-23"

keywords: openshift, kubernetes, node scaling, ca, autoscaler

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}



# Classic flavors
{: #classic-flavors}

Review the classic worker node flavors by metro.







## Amsterdam (`ams`)
{: #amsterdam}

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| b3c.16x64 | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.16x64.300gb | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 300GB SSD | N/A|
| b3c.32x128 | 32, 128GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.4x16 | 4, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.56x242 | 56, 242GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.8x32 | 8, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Balanced flavors in Amsterdam." caption-side="bottom"}
{: #ams-balanced-table}
{: tab-title="Balanced"}
{: tab-group="ams-tables"}


| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| c3c.16x16 | 16, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.16x32 | 16, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x32 | 32, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x64 | 32, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Compute flavors in Amsterdam." caption-side="bottom"}
{: #ams-compute-table}
{: tab-title="Compute"}
{: tab-group="ams-tables"}



| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| m3c.4x32 | 4, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| mb4c.20x192 | 20, 192GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x384 | 20, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x64 | 20, 64GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x64.2x1.9tb.ssd | 20, 64GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.32x384.3.8tb.ssd | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 1920GB SSD | N/A|
| mb4c.32x384.6x3.8tb.ssd | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 1920GB SSD | N/A|
| mb4c.32x768.3.8tb.ssd | 32, 768GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.48x1536 | 48, 1536GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| me4c.4x32 | 4, 32GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 2000GB HDD | N/A|
| me4c.4x32.1.9tb.ssd | 4, 32GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mg4c.32x384.2xp100 | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |2 P100 |
| mg4c.48x384.2xv100 | 48, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |2 V100 |
{: class="simple-tab-table"}
{: caption="Table. Memory flavors in Amsterdam." caption-side="bottom"}
{: #ams-memory-table}
{: tab-title="Memory"}
{: tab-group="ams-tables"}



| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| u3c.2x4 | 2, 4GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Ultra High Memory flavors in Amsterdam." caption-side="bottom"}
{: #ams-uhmemory-table}
{: tab-title="Ultra High Memory"}
{: tab-group="ams-tables"}





## Chennai (`che`)
{: #chennai}

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| b3c.16x64 | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.16x64.300gb | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 300GB SSD | N/A|
| b3c.32x128 | 32, 128GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.4x16 | 4, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.56x242 | 56, 242GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.8x32 | 8, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Balanced flavors in Chennai." caption-side="bottom"}
{: #che-balanced-table}
{: tab-title="Balanced"}
{: tab-group="che-tables"}


| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| c3c.16x16 | 16, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.16x32 | 16, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x32 | 32, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x64 | 32, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Compute flavors in Chennai." caption-side="bottom"}
{: #che-compute-table}
{: tab-title="Compute"}
{: tab-group="che-tables"}



| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| m3c.4x32 | 4, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| mb4c.20x192 | 20, 192GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x384 | 20, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x64 | 20, 64GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x64.2x1.9tb.ssd | 20, 64GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.32x384.3.8tb.ssd | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 1920GB SSD | N/A|
| mb4c.32x384.6x3.8tb.ssd | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 1920GB SSD | N/A|
| mb4c.32x768.3.8tb.ssd | 32, 768GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.48x1536 | 48, 1536GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| me4c.4x32 | 4, 32GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 2000GB HDD | N/A|
| me4c.4x32.1.9tb.ssd | 4, 32GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mg4c.32x384.2xp100 | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |2 P100 |
| mg4c.48x384.2xv100 | 48, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |2 V100 |
{: class="simple-tab-table"}
{: caption="Table. Memory flavors in Chennai." caption-side="bottom"}
{: #che-memory-table}
{: tab-title="Memory"}
{: tab-group="che-tables"}



| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| u3c.2x4 | 2, 4GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Ultra High Memory flavors in Chennai." caption-side="bottom"}
{: #che-uhmemory-table}
{: tab-title="Ultra High Memory"}
{: tab-group="che-tables"}





## Dallas (`dal`)
{: #dallas}

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| b3c.16x64 | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.16x64.300gb | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 300GB SSD | N/A|
| b3c.32x128 | 32, 128GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.4x16 | 4, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.56x242 | 56, 242GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.8x32 | 8, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Balanced flavors in Dallas." caption-side="bottom"}
{: #dal-balanced-table}
{: tab-title="Balanced"}
{: tab-group="dal-tables"}


| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| c3c.16x16 | 16, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.16x32 | 16, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x32 | 32, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x64 | 32, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Compute flavors in Dallas." caption-side="bottom"}
{: #dal-compute-table}
{: tab-title="Compute"}
{: tab-group="dal-tables"}



| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| m3c.16x128 | 16, 128GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| m3c.30x240 | 30, 240GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| m3c.48x384 | 48, 384GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| m3c.4x32 | 4, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| m3c.56x448 | 56, 448GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| m3c.64x512 | 64, 512GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| m3c.8x64 | 8, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| mb4c.20x192 | 20, 192GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x384 | 20, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x64 | 20, 64GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x64.2x1.9tb.ssd | 20, 64GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.32x384.3.8tb.ssd | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 1920GB SSD | N/A|
| mb4c.32x384.6x3.8tb.ssd | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 1920GB SSD | N/A|
| mb4c.32x768.3.8tb.ssd | 32, 768GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.48x1536 | 48, 1536GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| me4c.4x32 | 4, 32GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 2000GB HDD | N/A|
| me4c.4x32.1.9tb.ssd | 4, 32GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mg4c.32x384.2xp100 | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |2 P100 |
| mg4c.48x384.2xv100 | 48, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |2 V100 |
{: class="simple-tab-table"}
{: caption="Table. Memory flavors in Dallas." caption-side="bottom"}
{: #dal-memory-table}
{: tab-title="Memory"}
{: tab-group="dal-tables"}



| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| u3c.2x4 | 2, 4GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Ultra High Memory flavors in Dallas." caption-side="bottom"}
{: #dal-uhmemory-table}
{: tab-title="Ultra High Memory"}
{: tab-group="dal-tables"}





## France (`fra`)
{: #france}

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| b3c.16x64 | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.16x64.300gb | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 300GB SSD | N/A|
| b3c.32x128 | 32, 128GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.4x16 | 4, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.56x242 | 56, 242GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.8x32 | 8, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Balanced flavors in France." caption-side="bottom"}
{: #fra-balanced-table}
{: tab-title="Balanced"}
{: tab-group="fra-tables"}


| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| c3c.16x16 | 16, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.16x32 | 16, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x32 | 32, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x64 | 32, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Compute flavors in France." caption-side="bottom"}
{: #fra-compute-table}
{: tab-title="Compute"}
{: tab-group="fra-tables"}



| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| m3c.16x128 | 16, 128GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| m3c.30x240 | 30, 240GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| m3c.4x32 | 4, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| m3c.8x64 | 8, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| mb4c.20x192 | 20, 192GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x384 | 20, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x64 | 20, 64GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x64.2x1.9tb.ssd | 20, 64GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.32x384.3.8tb.ssd | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 1920GB SSD | N/A|
| mb4c.32x384.6x3.8tb.ssd | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 1920GB SSD | N/A|
| mb4c.32x768.3.8tb.ssd | 32, 768GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.48x1536 | 48, 1536GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| me4c.4x32 | 4, 32GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 2000GB HDD | N/A|
| me4c.4x32.1.9tb.ssd | 4, 32GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mg4c.32x384.2xp100 | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |2 P100 |
| mg4c.48x384.2xv100 | 48, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |2 V100 |
{: class="simple-tab-table"}
{: caption="Table. Memory flavors in France." caption-side="bottom"}
{: #fra-memory-table}
{: tab-title="Memory"}
{: tab-group="fra-tables"}



| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| u3c.2x4 | 2, 4GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Ultra High Memory flavors in France." caption-side="bottom"}
{: #fra-uhmemory-table}
{: tab-title="Ultra High Memory"}
{: tab-group="fra-tables"}





## London (`lon`)
{: #london}

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| b3c.16x64 | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.16x64.300gb | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 300GB SSD | N/A|
| b3c.32x128 | 32, 128GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.4x16 | 4, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.56x242 | 56, 242GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.8x32 | 8, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Balanced flavors in London." caption-side="bottom"}
{: #lon-balanced-table}
{: tab-title="Balanced"}
{: tab-group="lon-tables"}


| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| c3c.16x16 | 16, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.16x32 | 16, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x32 | 32, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x64 | 32, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Compute flavors in London." caption-side="bottom"}
{: #lon-compute-table}
{: tab-title="Compute"}
{: tab-group="lon-tables"}



| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| m3c.16x128 | 16, 128GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| m3c.30x240 | 30, 240GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| m3c.4x32 | 4, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| m3c.8x64 | 8, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| mb4c.20x192 | 20, 192GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x384 | 20, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x64 | 20, 64GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x64.2x1.9tb.ssd | 20, 64GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.32x384.3.8tb.ssd | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 1920GB SSD | N/A|
| mb4c.32x384.6x3.8tb.ssd | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 1920GB SSD | N/A|
| mb4c.32x768.3.8tb.ssd | 32, 768GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.48x1536 | 48, 1536GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| me4c.4x32 | 4, 32GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 2000GB HDD | N/A|
| me4c.4x32.1.9tb.ssd | 4, 32GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mg4c.32x384.2xp100 | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |2 P100 |
| mg4c.48x384.2xv100 | 48, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |2 V100 |
{: class="simple-tab-table"}
{: caption="Table. Memory flavors in London." caption-side="bottom"}
{: #lon-memory-table}
{: tab-title="Memory"}
{: tab-group="lon-tables"}



| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| u3c.2x4 | 2, 4GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Ultra High Memory flavors in London." caption-side="bottom"}
{: #lon-uhmemory-table}
{: tab-title="Ultra High Memory"}
{: tab-group="lon-tables"}





## Milan (`mil`)
{: #milan}

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| b3c.16x64 | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.16x64.300gb | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 300GB SSD | N/A|
| b3c.32x128 | 32, 128GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.4x16 | 4, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.56x242 | 56, 242GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.8x32 | 8, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Balanced flavors in Milan." caption-side="bottom"}
{: #mil-balanced-table}
{: tab-title="Balanced"}
{: tab-group="mil-tables"}


| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| c3c.16x16 | 16, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.16x32 | 16, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x32 | 32, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x64 | 32, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Compute flavors in Milan." caption-side="bottom"}
{: #mil-compute-table}
{: tab-title="Compute"}
{: tab-group="mil-tables"}



| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| m3c.4x32 | 4, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| mb4c.20x192 | 20, 192GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x384 | 20, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x64 | 20, 64GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x64.2x1.9tb.ssd | 20, 64GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.32x384.3.8tb.ssd | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 1920GB SSD | N/A|
| mb4c.32x384.6x3.8tb.ssd | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 1920GB SSD | N/A|
| mb4c.32x768.3.8tb.ssd | 32, 768GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.48x1536 | 48, 1536GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| me4c.4x32 | 4, 32GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 2000GB HDD | N/A|
| me4c.4x32.1.9tb.ssd | 4, 32GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mg4c.32x384.2xp100 | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |2 P100 |
| mg4c.48x384.2xv100 | 48, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |2 V100 |
{: class="simple-tab-table"}
{: caption="Table. Memory flavors in Milan." caption-side="bottom"}
{: #mil-memory-table}
{: tab-title="Memory"}
{: tab-group="mil-tables"}



| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| u3c.2x4 | 2, 4GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Ultra High Memory flavors in Milan." caption-side="bottom"}
{: #mil-uhmemory-table}
{: tab-title="Ultra High Memory"}
{: tab-group="mil-tables"}





## Montreal (`mon`)
{: #montreal}

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| b3c.16x64 | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.16x64.300gb | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 300GB SSD | N/A|
| b3c.32x128 | 32, 128GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.4x16 | 4, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.56x242 | 56, 242GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.8x32 | 8, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Balanced flavors in Montreal." caption-side="bottom"}
{: #mon-balanced-table}
{: tab-title="Balanced"}
{: tab-group="mon-tables"}


| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| c3c.16x16 | 16, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.16x32 | 16, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x32 | 32, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x64 | 32, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Compute flavors in Montreal." caption-side="bottom"}
{: #mon-compute-table}
{: tab-title="Compute"}
{: tab-group="mon-tables"}



| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| m3c.4x32 | 4, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| mb4c.20x192 | 20, 192GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x384 | 20, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x64 | 20, 64GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x64.2x1.9tb.ssd | 20, 64GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.32x384.3.8tb.ssd | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 1920GB SSD | N/A|
| mb4c.32x384.6x3.8tb.ssd | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 1920GB SSD | N/A|
| mb4c.32x768.3.8tb.ssd | 32, 768GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.48x1536 | 48, 1536GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| me4c.4x32 | 4, 32GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 2000GB HDD | N/A|
| me4c.4x32.1.9tb.ssd | 4, 32GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mg4c.32x384.2xp100 | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |2 P100 |
| mg4c.48x384.2xv100 | 48, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |2 V100 |
{: class="simple-tab-table"}
{: caption="Table. Memory flavors in Montreal." caption-side="bottom"}
{: #mon-memory-table}
{: tab-title="Memory"}
{: tab-group="mon-tables"}



| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| u3c.2x4 | 2, 4GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Ultra High Memory flavors in Montreal." caption-side="bottom"}
{: #mon-uhmemory-table}
{: tab-title="Ultra High Memory"}
{: tab-group="mon-tables"}





## Osaka (`osa`)
{: #osaka}

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| b3c.16x64 | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.16x64.300gb | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 300GB SSD | N/A|
| b3c.32x128 | 32, 128GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.4x16 | 4, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.56x242 | 56, 242GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.8x32 | 8, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Balanced flavors in Osaka." caption-side="bottom"}
{: #osa-balanced-table}
{: tab-title="Balanced"}
{: tab-group="osa-tables"}


| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| c3c.16x16 | 16, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.16x32 | 16, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x32 | 32, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x64 | 32, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Compute flavors in Osaka." caption-side="bottom"}
{: #osa-compute-table}
{: tab-title="Compute"}
{: tab-group="osa-tables"}



| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| m3c.16x128 | 16, 128GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| m3c.30x240 | 30, 240GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| m3c.48x384 | 48, 384GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| m3c.4x32 | 4, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| m3c.56x448 | 56, 448GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| m3c.64x512 | 64, 512GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| m3c.8x64 | 8, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| mb4c.20x192 | 20, 192GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x384 | 20, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x64 | 20, 64GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x64.2x1.9tb.ssd | 20, 64GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.32x384.3.8tb.ssd | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 1920GB SSD | N/A|
| mb4c.32x384.6x3.8tb.ssd | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 1920GB SSD | N/A|
| mb4c.32x768.3.8tb.ssd | 32, 768GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.48x1536 | 48, 1536GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| me4c.4x32 | 4, 32GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 2000GB HDD | N/A|
| me4c.4x32.1.9tb.ssd | 4, 32GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mg4c.32x384.2xp100 | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |2 P100 |
| mg4c.48x384.2xv100 | 48, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |2 V100 |
{: class="simple-tab-table"}
{: caption="Table. Memory flavors in Osaka." caption-side="bottom"}
{: #osa-memory-table}
{: tab-title="Memory"}
{: tab-group="osa-tables"}



| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| u3c.2x4 | 2, 4GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Ultra High Memory flavors in Osaka." caption-side="bottom"}
{: #osa-uhmemory-table}
{: tab-title="Ultra High Memory"}
{: tab-group="osa-tables"}





## Paris (`par`)
{: #paris}

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| b3c.16x64 | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.16x64.300gb | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 300GB SSD | N/A|
| b3c.32x128 | 32, 128GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.4x16 | 4, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.56x242 | 56, 242GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.8x32 | 8, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Balanced flavors in Paris." caption-side="bottom"}
{: #par-balanced-table}
{: tab-title="Balanced"}
{: tab-group="par-tables"}


| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| c3c.16x16 | 16, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.16x32 | 16, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x32 | 32, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x64 | 32, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Compute flavors in Paris." caption-side="bottom"}
{: #par-compute-table}
{: tab-title="Compute"}
{: tab-group="par-tables"}



| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| m3c.16x128 | 16, 128GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| m3c.30x240 | 30, 240GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| m3c.4x32 | 4, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| m3c.8x64 | 8, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| mb4c.20x192 | 20, 192GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x384 | 20, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x64 | 20, 64GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x64.2x1.9tb.ssd | 20, 64GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.32x384.3.8tb.ssd | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 1920GB SSD | N/A|
| mb4c.32x384.6x3.8tb.ssd | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 1920GB SSD | N/A|
| mb4c.32x768.3.8tb.ssd | 32, 768GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.48x1536 | 48, 1536GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| me4c.4x32 | 4, 32GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 2000GB HDD | N/A|
| me4c.4x32.1.9tb.ssd | 4, 32GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mg4c.32x384.2xp100 | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |2 P100 |
| mg4c.48x384.2xv100 | 48, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |2 V100 |
{: class="simple-tab-table"}
{: caption="Table. Memory flavors in Paris." caption-side="bottom"}
{: #par-memory-table}
{: tab-title="Memory"}
{: tab-group="par-tables"}



| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| u3c.2x4 | 2, 4GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Ultra High Memory flavors in Paris." caption-side="bottom"}
{: #par-uhmemory-table}
{: tab-title="Ultra High Memory"}
{: tab-group="par-tables"}





## South America (`sao`)
{: #south-america}

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| b3c.16x64 | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.16x64.300gb | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 300GB SSD | N/A|
| b3c.32x128 | 32, 128GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.4x16 | 4, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.56x242 | 56, 242GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.8x32 | 8, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Balanced flavors in South America." caption-side="bottom"}
{: #sao-balanced-table}
{: tab-title="Balanced"}
{: tab-group="sao-tables"}




| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| m3c.4x32 | 4, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Memory flavors in South America." caption-side="bottom"}
{: #sao-memory-table}
{: tab-title="Memory"}
{: tab-group="sao-tables"}



| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| u3c.2x4 | 2, 4GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Ultra High Memory flavors in South America." caption-side="bottom"}
{: #sao-uhmemory-table}
{: tab-title="Ultra High Memory"}
{: tab-group="sao-tables"}





## San Jose (`sjc`)
{: #san-jose}

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| b3c.16x64 | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.16x64.300gb | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 300GB SSD | N/A|
| b3c.32x128 | 32, 128GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.4x16 | 4, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.56x242 | 56, 242GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.8x32 | 8, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Balanced flavors in San Jose." caption-side="bottom"}
{: #sjc-balanced-table}
{: tab-title="Balanced"}
{: tab-group="sjc-tables"}


| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| c3c.16x16 | 16, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.16x32 | 16, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x32 | 32, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x64 | 32, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Compute flavors in San Jose." caption-side="bottom"}
{: #sjc-compute-table}
{: tab-title="Compute"}
{: tab-group="sjc-tables"}



| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| m3c.4x32 | 4, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Memory flavors in San Jose." caption-side="bottom"}
{: #sjc-memory-table}
{: tab-title="Memory"}
{: tab-group="sjc-tables"}



| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| u3c.2x4 | 2, 4GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Ultra High Memory flavors in San Jose." caption-side="bottom"}
{: #sjc-uhmemory-table}
{: tab-title="Ultra High Memory"}
{: tab-group="sjc-tables"}





## Singapore (`sng`)
{: #singapore}

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| b3c.16x64 | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.16x64.300gb | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 300GB SSD | N/A|
| b3c.4x16 | 4, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.8x32 | 8, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Balanced flavors in Singapore." caption-side="bottom"}
{: #sng-balanced-table}
{: tab-title="Balanced"}
{: tab-group="sng-tables"}


| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| c3c.16x16 | 16, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.16x32 | 16, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Compute flavors in Singapore." caption-side="bottom"}
{: #sng-compute-table}
{: tab-title="Compute"}
{: tab-group="sng-tables"}



| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| m3c.4x32 | 4, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Memory flavors in Singapore." caption-side="bottom"}
{: #sng-memory-table}
{: tab-title="Memory"}
{: tab-group="sng-tables"}



| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| u3c.2x4 | 2, 4GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Ultra High Memory flavors in Singapore." caption-side="bottom"}
{: #sng-uhmemory-table}
{: tab-title="Ultra High Memory"}
{: tab-group="sng-tables"}





## Sydney (`syd`)
{: #sydney}

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| b3c.16x64 | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.16x64.300gb | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 300GB SSD | N/A|
| b3c.32x128 | 32, 128GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.4x16 | 4, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.56x242 | 56, 242GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.8x32 | 8, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Balanced flavors in Sydney." caption-side="bottom"}
{: #syd-balanced-table}
{: tab-title="Balanced"}
{: tab-group="syd-tables"}


| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| c3c.16x16 | 16, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.16x32 | 16, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x32 | 32, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x64 | 32, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Compute flavors in Sydney." caption-side="bottom"}
{: #syd-compute-table}
{: tab-title="Compute"}
{: tab-group="syd-tables"}



| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| m3c.16x128 | 16, 128GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| m3c.30x240 | 30, 240GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| m3c.4x32 | 4, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| m3c.8x64 | 8, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| mb4c.20x192 | 20, 192GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x384 | 20, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x64 | 20, 64GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x64.2x1.9tb.ssd | 20, 64GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.32x384.3.8tb.ssd | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 1920GB SSD | N/A|
| mb4c.32x384.6x3.8tb.ssd | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 1920GB SSD | N/A|
| mb4c.32x768.3.8tb.ssd | 32, 768GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.48x1536 | 48, 1536GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| me4c.4x32 | 4, 32GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 2000GB HDD | N/A|
| me4c.4x32.1.9tb.ssd | 4, 32GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mg4c.32x384.2xp100 | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |2 P100 |
| mg4c.48x384.2xv100 | 48, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |2 V100 |
{: class="simple-tab-table"}
{: caption="Table. Memory flavors in Sydney." caption-side="bottom"}
{: #syd-memory-table}
{: tab-title="Memory"}
{: tab-group="syd-tables"}



| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| u3c.2x4 | 2, 4GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Ultra High Memory flavors in Sydney." caption-side="bottom"}
{: #syd-uhmemory-table}
{: tab-title="Ultra High Memory"}
{: tab-group="syd-tables"}





## Tokyo (`tok`)
{: #tokyo}

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| b3c.16x64 | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.16x64.300gb | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 300GB SSD | N/A|
| b3c.32x128 | 32, 128GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.4x16 | 4, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.56x242 | 56, 242GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.8x32 | 8, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Balanced flavors in Tokyo." caption-side="bottom"}
{: #tok-balanced-table}
{: tab-title="Balanced"}
{: tab-group="tok-tables"}


| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| c3c.16x16 | 16, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.16x32 | 16, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x32 | 32, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x64 | 32, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Compute flavors in Tokyo." caption-side="bottom"}
{: #tok-compute-table}
{: tab-title="Compute"}
{: tab-group="tok-tables"}



| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| m3c.16x128 | 16, 128GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| m3c.30x240 | 30, 240GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| m3c.4x32 | 4, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| m3c.8x64 | 8, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| mb4c.20x192 | 20, 192GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x384 | 20, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x64 | 20, 64GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x64.2x1.9tb.ssd | 20, 64GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.32x384.3.8tb.ssd | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 1920GB SSD | N/A|
| mb4c.32x384.6x3.8tb.ssd | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 1920GB SSD | N/A|
| mb4c.32x768.3.8tb.ssd | 32, 768GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.48x1536 | 48, 1536GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| me4c.4x32 | 4, 32GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 2000GB HDD | N/A|
| me4c.4x32.1.9tb.ssd | 4, 32GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mg4c.32x384.2xp100 | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |2 P100 |
| mg4c.48x384.2xv100 | 48, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |2 V100 |
{: class="simple-tab-table"}
{: caption="Table. Memory flavors in Tokyo." caption-side="bottom"}
{: #tok-memory-table}
{: tab-title="Memory"}
{: tab-group="tok-tables"}



| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| u3c.2x4 | 2, 4GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Ultra High Memory flavors in Tokyo." caption-side="bottom"}
{: #tok-uhmemory-table}
{: tab-title="Ultra High Memory"}
{: tab-group="tok-tables"}





## Toronto (`tor`)
{: #toronto}

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| b3c.16x64 | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.16x64.300gb | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 300GB SSD | N/A|
| b3c.32x128 | 32, 128GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.4x16 | 4, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.56x242 | 56, 242GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.8x32 | 8, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Balanced flavors in Toronto." caption-side="bottom"}
{: #tor-balanced-table}
{: tab-title="Balanced"}
{: tab-group="tor-tables"}


| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| c3c.16x16 | 16, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.16x32 | 16, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x32 | 32, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x64 | 32, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Compute flavors in Toronto." caption-side="bottom"}
{: #tor-compute-table}
{: tab-title="Compute"}
{: tab-group="tor-tables"}



| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| m3c.16x128 | 16, 128GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| m3c.30x240 | 30, 240GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| m3c.4x32 | 4, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| m3c.8x64 | 8, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| mb4c.20x192 | 20, 192GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x384 | 20, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x64 | 20, 64GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x64.2x1.9tb.ssd | 20, 64GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.32x384.3.8tb.ssd | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 1920GB SSD | N/A|
| mb4c.32x384.6x3.8tb.ssd | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 1920GB SSD | N/A|
| mb4c.32x768.3.8tb.ssd | 32, 768GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.48x1536 | 48, 1536GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| me4c.4x32 | 4, 32GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 2000GB HDD | N/A|
| me4c.4x32.1.9tb.ssd | 4, 32GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mg4c.32x384.2xp100 | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |2 P100 |
| mg4c.48x384.2xv100 | 48, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |2 V100 |
{: class="simple-tab-table"}
{: caption="Table. Memory flavors in Toronto." caption-side="bottom"}
{: #tor-memory-table}
{: tab-title="Memory"}
{: tab-group="tor-tables"}



| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| u3c.2x4 | 2, 4GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Ultra High Memory flavors in Toronto." caption-side="bottom"}
{: #tor-uhmemory-table}
{: tab-title="Ultra High Memory"}
{: tab-group="tor-tables"}





## Washington DC (`wdc`)
{: #washington-dc}

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| b3c.16x64 | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.16x64.300gb | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 300GB SSD | N/A|
| b3c.32x128 | 32, 128GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.4x16 | 4, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.56x242 | 56, 242GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.8x32 | 8, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Balanced flavors in Washington DC." caption-side="bottom"}
{: #wdc-balanced-table}
{: tab-title="Balanced"}
{: tab-group="wdc-tables"}


| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| c3c.16x16 | 16, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.16x32 | 16, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x32 | 32, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x64 | 32, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Compute flavors in Washington DC." caption-side="bottom"}
{: #wdc-compute-table}
{: tab-title="Compute"}
{: tab-group="wdc-tables"}



| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| m3c.16x128 | 16, 128GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| m3c.30x240 | 30, 240GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| m3c.4x32 | 4, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| m3c.8x64 | 8, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| mb4c.20x192 | 20, 192GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x384 | 20, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x64 | 20, 64GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.20x64.2x1.9tb.ssd | 20, 64GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.32x384.3.8tb.ssd | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 1920GB SSD | N/A|
| mb4c.32x384.6x3.8tb.ssd | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 1920GB SSD | N/A|
| mb4c.32x768.3.8tb.ssd | 32, 768GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mb4c.48x1536 | 48, 1536GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| me4c.4x32 | 4, 32GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 2000GB HDD | N/A|
| me4c.4x32.1.9tb.ssd | 4, 32GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD | N/A|
| mg4c.32x384.2xp100 | 32, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |2 P100 |
| mg4c.48x384.2xv100 | 48, 384GB, 10000Mbps | Physical | REDHAT_7_64, **REDHAT_8_64 (default)**| 2000GB HDD | 960GB SSD |2 V100 |
{: class="simple-tab-table"}
{: caption="Table. Memory flavors in Washington DC." caption-side="bottom"}
{: #wdc-memory-table}
{: tab-title="Memory"}
{: tab-group="wdc-tables"}



| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| u3c.2x4 | 2, 4GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Ultra High Memory flavors in Washington DC." caption-side="bottom"}
{: #wdc-uhmemory-table}
{: tab-title="Ultra High Memory"}
{: tab-group="wdc-tables"}








