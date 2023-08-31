---

copyright: 
  years: 2014, 2023
lastupdated: "2023-08-31"

keywords: openshift, node scaling, ca, autoscaler

subcollection: openshift


---



{{site.data.keyword.attribute-definition-list}}



# VPC flavors
{: #vpc-flavors}

Review the VPC Gen 2 worker node flavors by metro.

 



## `au-syd`
{: #au-syd}

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |
| bx2.16x64 | 16, 64GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.2x8 | 2, 8GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A|
| bx2.32x128 | 32, 128GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.48x192 | 48, 192GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.4x16 | 4, 16GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| bx2.8x32 | 8, 32GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.16x32 | 16, 32GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.2x4 | 2, 4GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A|
| cx2.32x64 | 32, 64GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.48x96 | 48, 96GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.4x8 | 4, 8GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| cx2.8x16 | 8, 16GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.128x1024 | 128, 1024GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.16x128 | 16, 128GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.16x128.2000gb | 16, 128GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | 2000GB BLOCK | N/A|
| mx2.2x16 | 2, 16GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A|
| mx2.32x256 | 32, 256GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.48x384 | 48, 384GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.4x32 | 4, 32GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| mx2.64x512 | 64, 512GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.8x64 | 8, 64GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
{: caption="Table 1. Worker node flavors for Australia." caption-side="bottom"}



## `br-sao`
{: #br-sao}

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |
| bx2.16x64 | 16, 64GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.2x8 | 2, 8GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A|
| bx2.32x128 | 32, 128GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.48x192 | 48, 192GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.4x16 | 4, 16GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| bx2.8x32 | 8, 32GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.16x32 | 16, 32GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.2x4 | 2, 4GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A|
| cx2.32x64 | 32, 64GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.48x96 | 48, 96GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.4x8 | 4, 8GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| cx2.8x16 | 8, 16GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.128x1024 | 128, 1024GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.16x128 | 16, 128GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.2x16 | 2, 16GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A|
| mx2.32x256 | 32, 256GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.48x384 | 48, 384GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.4x32 | 4, 32GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| mx2.64x512 | 64, 512GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.8x64 | 8, 64GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
{: caption="Table 2. Worker node flavors for Brazil." caption-side="bottom"}



## `ca-tor`
{: #ca-tor}

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |
| bx2.16x64 | 16, 64GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.2x8 | 2, 8GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A|
| bx2.32x128 | 32, 128GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.48x192 | 48, 192GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.4x16 | 4, 16GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| bx2.8x32 | 8, 32GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.16x32 | 16, 32GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.2x4 | 2, 4GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A|
| cx2.32x64 | 32, 64GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.48x96 | 48, 96GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.4x8 | 4, 8GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| cx2.8x16 | 8, 16GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.128x1024 | 128, 1024GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.16x128 | 16, 128GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.16x128.2000gb | 16, 128GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | 2000GB BLOCK | N/A|
| mx2.2x16 | 2, 16GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A|
| mx2.32x256 | 32, 256GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.48x384 | 48, 384GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.4x32 | 4, 32GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| mx2.64x512 | 64, 512GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.8x64 | 8, 64GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
{: caption="Table 3. Worker node flavors for Canada." caption-side="bottom"}



## `eu-de`
{: #eu-de}

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |
| bx2.16x64 | 16, 64GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.2x8 | 2, 8GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A|
| bx2.32x128 | 32, 128GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.48x192 | 48, 192GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.4x16 | 4, 16GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| bx2.8x32 | 8, 32GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.16x32 | 16, 32GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.2x4 | 2, 4GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A|
| cx2.32x64 | 32, 64GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.48x96 | 48, 96GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.4x8 | 4, 8GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| cx2.8x16 | 8, 16GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.128x1024 | 128, 1024GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.16x128 | 16, 128GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.16x128.2000gb | 16, 128GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | 2000GB BLOCK | N/A|
| mx2.2x16 | 2, 16GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A|
| mx2.32x256 | 32, 256GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.48x384 | 48, 384GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.4x32 | 4, 32GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| mx2.64x512 | 64, 512GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.8x64 | 8, 64GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
{: caption="Table 4. Worker node flavors for Europe." caption-side="bottom"}



## `eu-es`
{: #eu-es}

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |
| bx2.16x64 | 16, 64GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.2x8 | 2, 8GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A|
| bx2.32x128 | 32, 128GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.48x192 | 48, 192GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.4x16 | 4, 16GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| bx2.8x32 | 8, 32GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.16x32 | 16, 32GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.2x4 | 2, 4GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A|
| cx2.32x64 | 32, 64GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.48x96 | 48, 96GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.4x8 | 4, 8GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| cx2.8x16 | 8, 16GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.128x1024 | 128, 1024GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.16x128 | 16, 128GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.2x16 | 2, 16GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A|
| mx2.32x256 | 32, 256GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.48x384 | 48, 384GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.4x32 | 4, 32GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| mx2.64x512 | 64, 512GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.8x64 | 8, 64GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
{: caption="Table 5. Worker node flavors for Europe." caption-side="bottom"}



## `eu-gb`
{: #eu-gb}

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |
| bx2.16x64 | 16, 64GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.2x8 | 2, 8GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A|
| bx2.32x128 | 32, 128GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.48x192 | 48, 192GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.4x16 | 4, 16GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| bx2.8x32 | 8, 32GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.16x32 | 16, 32GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.2x4 | 2, 4GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A|
| cx2.32x64 | 32, 64GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.48x96 | 48, 96GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.4x8 | 4, 8GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| cx2.8x16 | 8, 16GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.128x1024 | 128, 1024GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.16x128 | 16, 128GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.16x128.2000gb | 16, 128GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | 2000GB BLOCK | N/A|
| mx2.2x16 | 2, 16GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A|
| mx2.32x256 | 32, 256GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.48x384 | 48, 384GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.4x32 | 4, 32GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| mx2.64x512 | 64, 512GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.8x64 | 8, 64GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
{: caption="Table 6. Worker node flavors for Europe." caption-side="bottom"}



## `jp-osa`
{: #jp-osa}

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |
| bx2.16x64 | 16, 64GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.2x8 | 2, 8GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A|
| bx2.32x128 | 32, 128GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.48x192 | 48, 192GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.4x16 | 4, 16GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| bx2.8x32 | 8, 32GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.16x32 | 16, 32GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.2x4 | 2, 4GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A|
| cx2.32x64 | 32, 64GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.48x96 | 48, 96GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.4x8 | 4, 8GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| cx2.8x16 | 8, 16GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.128x1024 | 128, 1024GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.16x128 | 16, 128GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.2x16 | 2, 16GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A|
| mx2.32x256 | 32, 256GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.48x384 | 48, 384GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.4x32 | 4, 32GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| mx2.64x512 | 64, 512GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.8x64 | 8, 64GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
{: caption="Table 7. Worker node flavors for Japan." caption-side="bottom"}



## `jp-tok`
{: #jp-tok}

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |
| bx2.16x64 | 16, 64GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.2x8 | 2, 8GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A|
| bx2.32x128 | 32, 128GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.48x192 | 48, 192GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.4x16 | 4, 16GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| bx2.8x32 | 8, 32GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.16x32 | 16, 32GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.2x4 | 2, 4GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A|
| cx2.32x64 | 32, 64GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.48x96 | 48, 96GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.4x8 | 4, 8GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| cx2.8x16 | 8, 16GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.128x1024 | 128, 1024GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.16x128 | 16, 128GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.16x128.2000gb | 16, 128GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | 2000GB BLOCK | N/A|
| mx2.2x16 | 2, 16GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A|
| mx2.32x256 | 32, 256GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.48x384 | 48, 384GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.4x32 | 4, 32GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| mx2.64x512 | 64, 512GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.8x64 | 8, 64GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
{: caption="Table 8. Worker node flavors for Japan." caption-side="bottom"}



## `us-east`
{: #us-east}

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |
| bx2.16x64 | 16, 64GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.2x8 | 2, 8GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A|
| bx2.32x128 | 32, 128GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.48x192 | 48, 192GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.4x16 | 4, 16GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| bx2.8x32 | 8, 32GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.16x32 | 16, 32GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.2x4 | 2, 4GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A|
| cx2.32x64 | 32, 64GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.48x96 | 48, 96GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.4x8 | 4, 8GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| cx2.8x16 | 8, 16GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.128x1024 | 128, 1024GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.16x128 | 16, 128GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.16x128.2000gb | 16, 128GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | 2000GB BLOCK | N/A|
| mx2.2x16 | 2, 16GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A|
| mx2.32x256 | 32, 256GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.48x384 | 48, 384GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.4x32 | 4, 32GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| mx2.64x512 | 64, 512GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.8x64 | 8, 64GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
{: caption="Table 9. Worker node flavors for United States." caption-side="bottom"}



## `us-south`
{: #us-south}

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |
| bx2.16x64 | 16, 64GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.2x8 | 2, 8GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A|
| bx2.32x128 | 32, 128GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.48x192 | 48, 192GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.4x16 | 4, 16GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| bx2.8x32 | 8, 32GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.16x32 | 16, 32GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.2x4 | 2, 4GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A|
| cx2.32x64 | 32, 64GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.48x96 | 48, 96GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.4x8 | 4, 8GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| cx2.8x16 | 8, 16GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.128x1024 | 128, 1024GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.16x128 | 16, 128GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.16x128.2000gb | 16, 128GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | 2000GB BLOCK | N/A|
| mx2.2x16 | 2, 16GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A|
| mx2.32x256 | 32, 256GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.48x384 | 48, 384GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.4x32 | 4, 32GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| mx2.64x512 | 64, 512GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.8x64 | 8, 64GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
{: caption="Table 10. Worker node flavors for United States." caption-side="bottom"}




