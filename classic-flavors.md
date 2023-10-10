---

copyright: 
  years: 2014, 2023
lastupdated: "2023-10-10"

keywords: openshift, kubernetes, node scaling, ca, autoscaler

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}



# Classic flavors
{: #classic-flavors}

Review the classic worker node flavors by metro.







## `ams`
{: #ams}

### Amsterdam flavors
{: #ams-balanced}

Review the attributes for the Balanced worker node flavors.

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
{: tab-title="Balanced profiles"}
{: tab-group="ams-tables"}


### Amsterdam flavors
{: #ams-compute}

Review the attributes for the Compute worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| c3c.16x16 | 16, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.16x32 | 16, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x32 | 32, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x64 | 32, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Compute flavors in Amsterdam." caption-side="bottom"}
{: #ams-compute-table}
{: tab-title="Compute profiles"}
{: tab-group="ams-tables"}



### Amsterdam flavors
{: #ams-memory}

Review the attributes for the Memory worker node flavors.

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
{: tab-title="Memory profiles"}
{: tab-group="ams-tables"}



### Amsterdam flavors
{: #ams-uhmemory}

Review the attributes for the Ultra High Memory worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| u3c.2x4 | 2, 4GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Ultra High Memory flavors in Amsterdam." caption-side="bottom"}
{: #ams-uhmemory-table}
{: tab-title="Ultra High Memory profiles"}
{: tab-group="ams-tables"}





## `che`
{: #che}

### Chennai flavors
{: #che-balanced}

Review the attributes for the Balanced worker node flavors.

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
{: tab-title="Balanced profiles"}
{: tab-group="che-tables"}


### Chennai flavors
{: #che-compute}

Review the attributes for the Compute worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| c3c.16x16 | 16, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.16x32 | 16, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x32 | 32, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x64 | 32, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Compute flavors in Chennai." caption-side="bottom"}
{: #che-compute-table}
{: tab-title="Compute profiles"}
{: tab-group="che-tables"}



### Chennai flavors
{: #che-memory}

Review the attributes for the Memory worker node flavors.

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
{: tab-title="Memory profiles"}
{: tab-group="che-tables"}



### Chennai flavors
{: #che-uhmemory}

Review the attributes for the Ultra High Memory worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| u3c.2x4 | 2, 4GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Ultra High Memory flavors in Chennai." caption-side="bottom"}
{: #che-uhmemory-table}
{: tab-title="Ultra High Memory profiles"}
{: tab-group="che-tables"}





## `dal`
{: #dal}

### Dallas flavors
{: #dal-balanced}

Review the attributes for the Balanced worker node flavors.

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
{: tab-title="Balanced profiles"}
{: tab-group="dal-tables"}


### Dallas flavors
{: #dal-compute}

Review the attributes for the Compute worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| c3c.16x16 | 16, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.16x32 | 16, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x32 | 32, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x64 | 32, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Compute flavors in Dallas." caption-side="bottom"}
{: #dal-compute-table}
{: tab-title="Compute profiles"}
{: tab-group="dal-tables"}



### Dallas flavors
{: #dal-memory}

Review the attributes for the Memory worker node flavors.

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
{: tab-title="Memory profiles"}
{: tab-group="dal-tables"}



### Dallas flavors
{: #dal-uhmemory}

Review the attributes for the Ultra High Memory worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| u3c.2x4 | 2, 4GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Ultra High Memory flavors in Dallas." caption-side="bottom"}
{: #dal-uhmemory-table}
{: tab-title="Ultra High Memory profiles"}
{: tab-group="dal-tables"}





## `fra`
{: #fra}

### France flavors
{: #fra-balanced}

Review the attributes for the Balanced worker node flavors.

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
{: tab-title="Balanced profiles"}
{: tab-group="fra-tables"}


### France flavors
{: #fra-compute}

Review the attributes for the Compute worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| c3c.16x16 | 16, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.16x32 | 16, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x32 | 32, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x64 | 32, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Compute flavors in France." caption-side="bottom"}
{: #fra-compute-table}
{: tab-title="Compute profiles"}
{: tab-group="fra-tables"}



### France flavors
{: #fra-memory}

Review the attributes for the Memory worker node flavors.

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
{: tab-title="Memory profiles"}
{: tab-group="fra-tables"}



### France flavors
{: #fra-uhmemory}

Review the attributes for the Ultra High Memory worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| u3c.2x4 | 2, 4GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Ultra High Memory flavors in France." caption-side="bottom"}
{: #fra-uhmemory-table}
{: tab-title="Ultra High Memory profiles"}
{: tab-group="fra-tables"}





## `lon`
{: #lon}

### London flavors
{: #lon-balanced}

Review the attributes for the Balanced worker node flavors.

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
{: tab-title="Balanced profiles"}
{: tab-group="lon-tables"}


### London flavors
{: #lon-compute}

Review the attributes for the Compute worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| c3c.16x16 | 16, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.16x32 | 16, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x32 | 32, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x64 | 32, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Compute flavors in London." caption-side="bottom"}
{: #lon-compute-table}
{: tab-title="Compute profiles"}
{: tab-group="lon-tables"}



### London flavors
{: #lon-memory}

Review the attributes for the Memory worker node flavors.

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
{: tab-title="Memory profiles"}
{: tab-group="lon-tables"}



### London flavors
{: #lon-uhmemory}

Review the attributes for the Ultra High Memory worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| u3c.2x4 | 2, 4GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Ultra High Memory flavors in London." caption-side="bottom"}
{: #lon-uhmemory-table}
{: tab-title="Ultra High Memory profiles"}
{: tab-group="lon-tables"}





## `mil`
{: #mil}

### Milan flavors
{: #mil-balanced}

Review the attributes for the Balanced worker node flavors.

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
{: tab-title="Balanced profiles"}
{: tab-group="mil-tables"}


### Milan flavors
{: #mil-compute}

Review the attributes for the Compute worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| c3c.16x16 | 16, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.16x32 | 16, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x32 | 32, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x64 | 32, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Compute flavors in Milan." caption-side="bottom"}
{: #mil-compute-table}
{: tab-title="Compute profiles"}
{: tab-group="mil-tables"}



### Milan flavors
{: #mil-memory}

Review the attributes for the Memory worker node flavors.

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
{: tab-title="Memory profiles"}
{: tab-group="mil-tables"}



### Milan flavors
{: #mil-uhmemory}

Review the attributes for the Ultra High Memory worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| u3c.2x4 | 2, 4GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Ultra High Memory flavors in Milan." caption-side="bottom"}
{: #mil-uhmemory-table}
{: tab-title="Ultra High Memory profiles"}
{: tab-group="mil-tables"}





## `mon`
{: #mon}

### Montreal flavors
{: #mon-balanced}

Review the attributes for the Balanced worker node flavors.

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
{: tab-title="Balanced profiles"}
{: tab-group="mon-tables"}


### Montreal flavors
{: #mon-compute}

Review the attributes for the Compute worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| c3c.16x16 | 16, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.16x32 | 16, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x32 | 32, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x64 | 32, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Compute flavors in Montreal." caption-side="bottom"}
{: #mon-compute-table}
{: tab-title="Compute profiles"}
{: tab-group="mon-tables"}



### Montreal flavors
{: #mon-memory}

Review the attributes for the Memory worker node flavors.

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
{: tab-title="Memory profiles"}
{: tab-group="mon-tables"}



### Montreal flavors
{: #mon-uhmemory}

Review the attributes for the Ultra High Memory worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| u3c.2x4 | 2, 4GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Ultra High Memory flavors in Montreal." caption-side="bottom"}
{: #mon-uhmemory-table}
{: tab-title="Ultra High Memory profiles"}
{: tab-group="mon-tables"}





## `osa`
{: #osa}

### Osaka flavors
{: #osa-balanced}

Review the attributes for the Balanced worker node flavors.

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
{: tab-title="Balanced profiles"}
{: tab-group="osa-tables"}


### Osaka flavors
{: #osa-compute}

Review the attributes for the Compute worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| c3c.16x16 | 16, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.16x32 | 16, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x32 | 32, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x64 | 32, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Compute flavors in Osaka." caption-side="bottom"}
{: #osa-compute-table}
{: tab-title="Compute profiles"}
{: tab-group="osa-tables"}



### Osaka flavors
{: #osa-memory}

Review the attributes for the Memory worker node flavors.

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
{: tab-title="Memory profiles"}
{: tab-group="osa-tables"}



### Osaka flavors
{: #osa-uhmemory}

Review the attributes for the Ultra High Memory worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| u3c.2x4 | 2, 4GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Ultra High Memory flavors in Osaka." caption-side="bottom"}
{: #osa-uhmemory-table}
{: tab-title="Ultra High Memory profiles"}
{: tab-group="osa-tables"}





## `par`
{: #par}

### Paris flavors
{: #par-balanced}

Review the attributes for the Balanced worker node flavors.

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
{: tab-title="Balanced profiles"}
{: tab-group="par-tables"}


### Paris flavors
{: #par-compute}

Review the attributes for the Compute worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| c3c.16x16 | 16, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.16x32 | 16, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x32 | 32, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x64 | 32, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Compute flavors in Paris." caption-side="bottom"}
{: #par-compute-table}
{: tab-title="Compute profiles"}
{: tab-group="par-tables"}



### Paris flavors
{: #par-memory}

Review the attributes for the Memory worker node flavors.

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
{: tab-title="Memory profiles"}
{: tab-group="par-tables"}



### Paris flavors
{: #par-uhmemory}

Review the attributes for the Ultra High Memory worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| u3c.2x4 | 2, 4GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Ultra High Memory flavors in Paris." caption-side="bottom"}
{: #par-uhmemory-table}
{: tab-title="Ultra High Memory profiles"}
{: tab-group="par-tables"}





## `sao`
{: #sao}

### South America flavors
{: #sao-balanced}

Review the attributes for the Balanced worker node flavors.

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
{: tab-title="Balanced profiles"}
{: tab-group="sao-tables"}




### South America flavors
{: #sao-memory}

Review the attributes for the Memory worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| m3c.4x32 | 4, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Memory flavors in South America." caption-side="bottom"}
{: #sao-memory-table}
{: tab-title="Memory profiles"}
{: tab-group="sao-tables"}



### South America flavors
{: #sao-uhmemory}

Review the attributes for the Ultra High Memory worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| u3c.2x4 | 2, 4GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Ultra High Memory flavors in South America." caption-side="bottom"}
{: #sao-uhmemory-table}
{: tab-title="Ultra High Memory profiles"}
{: tab-group="sao-tables"}





## `sjc`
{: #sjc}

### San Jose flavors
{: #sjc-balanced}

Review the attributes for the Balanced worker node flavors.

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
{: tab-title="Balanced profiles"}
{: tab-group="sjc-tables"}


### San Jose flavors
{: #sjc-compute}

Review the attributes for the Compute worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| c3c.16x16 | 16, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.16x32 | 16, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x32 | 32, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x64 | 32, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Compute flavors in San Jose." caption-side="bottom"}
{: #sjc-compute-table}
{: tab-title="Compute profiles"}
{: tab-group="sjc-tables"}



### San Jose flavors
{: #sjc-memory}

Review the attributes for the Memory worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| m3c.4x32 | 4, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Memory flavors in San Jose." caption-side="bottom"}
{: #sjc-memory-table}
{: tab-title="Memory profiles"}
{: tab-group="sjc-tables"}



### San Jose flavors
{: #sjc-uhmemory}

Review the attributes for the Ultra High Memory worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| u3c.2x4 | 2, 4GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Ultra High Memory flavors in San Jose." caption-side="bottom"}
{: #sjc-uhmemory-table}
{: tab-title="Ultra High Memory profiles"}
{: tab-group="sjc-tables"}





## `sng`
{: #sng}

### Singapore flavors
{: #sng-balanced}

Review the attributes for the Balanced worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| b3c.16x64 | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.16x64.300gb | 16, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 300GB SSD | N/A|
| b3c.4x16 | 4, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| b3c.8x32 | 8, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Balanced flavors in Singapore." caption-side="bottom"}
{: #sng-balanced-table}
{: tab-title="Balanced profiles"}
{: tab-group="sng-tables"}


### Singapore flavors
{: #sng-compute}

Review the attributes for the Compute worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| c3c.16x16 | 16, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.16x32 | 16, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Compute flavors in Singapore." caption-side="bottom"}
{: #sng-compute-table}
{: tab-title="Compute profiles"}
{: tab-group="sng-tables"}



### Singapore flavors
{: #sng-memory}

Review the attributes for the Memory worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| m3c.4x32 | 4, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Memory flavors in Singapore." caption-side="bottom"}
{: #sng-memory-table}
{: tab-title="Memory profiles"}
{: tab-group="sng-tables"}



### Singapore flavors
{: #sng-uhmemory}

Review the attributes for the Ultra High Memory worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| u3c.2x4 | 2, 4GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Ultra High Memory flavors in Singapore." caption-side="bottom"}
{: #sng-uhmemory-table}
{: tab-title="Ultra High Memory profiles"}
{: tab-group="sng-tables"}





## `syd`
{: #syd}

### Sydney flavors
{: #syd-balanced}

Review the attributes for the Balanced worker node flavors.

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
{: tab-title="Balanced profiles"}
{: tab-group="syd-tables"}


### Sydney flavors
{: #syd-compute}

Review the attributes for the Compute worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| c3c.16x16 | 16, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.16x32 | 16, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x32 | 32, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x64 | 32, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Compute flavors in Sydney." caption-side="bottom"}
{: #syd-compute-table}
{: tab-title="Compute profiles"}
{: tab-group="syd-tables"}



### Sydney flavors
{: #syd-memory}

Review the attributes for the Memory worker node flavors.

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
{: tab-title="Memory profiles"}
{: tab-group="syd-tables"}



### Sydney flavors
{: #syd-uhmemory}

Review the attributes for the Ultra High Memory worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| u3c.2x4 | 2, 4GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Ultra High Memory flavors in Sydney." caption-side="bottom"}
{: #syd-uhmemory-table}
{: tab-title="Ultra High Memory profiles"}
{: tab-group="syd-tables"}





## `tok`
{: #tok}

### Tokyo flavors
{: #tok-balanced}

Review the attributes for the Balanced worker node flavors.

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
{: tab-title="Balanced profiles"}
{: tab-group="tok-tables"}


### Tokyo flavors
{: #tok-compute}

Review the attributes for the Compute worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| c3c.16x16 | 16, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.16x32 | 16, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x32 | 32, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x64 | 32, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Compute flavors in Tokyo." caption-side="bottom"}
{: #tok-compute-table}
{: tab-title="Compute profiles"}
{: tab-group="tok-tables"}



### Tokyo flavors
{: #tok-memory}

Review the attributes for the Memory worker node flavors.

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
{: tab-title="Memory profiles"}
{: tab-group="tok-tables"}



### Tokyo flavors
{: #tok-uhmemory}

Review the attributes for the Ultra High Memory worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| u3c.2x4 | 2, 4GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Ultra High Memory flavors in Tokyo." caption-side="bottom"}
{: #tok-uhmemory-table}
{: tab-title="Ultra High Memory profiles"}
{: tab-group="tok-tables"}





## `tor`
{: #tor}

### Toronto flavors
{: #tor-balanced}

Review the attributes for the Balanced worker node flavors.

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
{: tab-title="Balanced profiles"}
{: tab-group="tor-tables"}


### Toronto flavors
{: #tor-compute}

Review the attributes for the Compute worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| c3c.16x16 | 16, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.16x32 | 16, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x32 | 32, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x64 | 32, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Compute flavors in Toronto." caption-side="bottom"}
{: #tor-compute-table}
{: tab-title="Compute profiles"}
{: tab-group="tor-tables"}



### Toronto flavors
{: #tor-memory}

Review the attributes for the Memory worker node flavors.

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
{: tab-title="Memory profiles"}
{: tab-group="tor-tables"}



### Toronto flavors
{: #tor-uhmemory}

Review the attributes for the Ultra High Memory worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| u3c.2x4 | 2, 4GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Ultra High Memory flavors in Toronto." caption-side="bottom"}
{: #tor-uhmemory-table}
{: tab-title="Ultra High Memory profiles"}
{: tab-group="tor-tables"}





## `wdc`
{: #wdc}

### Washington DC flavors
{: #wdc-balanced}

Review the attributes for the Balanced worker node flavors.

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
{: tab-title="Balanced profiles"}
{: tab-group="wdc-tables"}


### Washington DC flavors
{: #wdc-compute}

Review the attributes for the Compute worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| c3c.16x16 | 16, 16GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.16x32 | 16, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x32 | 32, 32GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
| c3c.32x64 | 32, 64GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Compute flavors in Washington DC." caption-side="bottom"}
{: #wdc-compute-table}
{: tab-title="Compute profiles"}
{: tab-group="wdc-tables"}



### Washington DC flavors
{: #wdc-memory}

Review the attributes for the Memory worker node flavors.

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
{: tab-title="Memory profiles"}
{: tab-group="wdc-tables"}



### Washington DC flavors
{: #wdc-uhmemory}

Review the attributes for the Ultra High Memory worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- | -- |
| u3c.2x4 | 2, 4GB, 1000Mbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 25GB SSD | 100GB SSD | N/A|
{: class="simple-tab-table"}
{: caption="Table. Ultra High Memory flavors in Washington DC." caption-side="bottom"}
{: #wdc-uhmemory-table}
{: tab-title="Ultra High Memory profiles"}
{: tab-group="wdc-tables"}








