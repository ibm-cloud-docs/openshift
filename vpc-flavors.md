---

copyright: 
  years: 2014, 2023
lastupdated: "2023-04-14"

keywords: openshift, node scaling, ca, autoscaler

subcollection: openshift


---



{{site.data.keyword.attribute-definition-list}}



# VPC flavors
{: #vpc-flavors}

Review the VPC Gen 2 worker node flavors by metro.





## `au-syd`
{: #au-syd}

| Name | Memory | Network speed | Cores | Type | OS | Primary storage | Secondary storage | Secondary storage options |
| -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- |
| bx2.16x64 | 64GB | 24Gbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.2x8 | 8GB | 4Gbps | 2 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | N/A|
| bx2.32x128 | 128GB | 25Gbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.48x192 | 192GB | 25Gbps | 48 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.4x16 | 16GB | 8Gbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| bx2.8x32 | 32GB | 16Gbps | 8 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.16x32 | 32GB | 24Gbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.2x4 | 4GB | 4Gbps | 2 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | N/A|
| cx2.32x64 | 64GB | 25Gbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.48x96 | 96GB | 25Gbps | 48 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.4x8 | 8GB | 8Gbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| cx2.8x16 | 16GB | 16Gbps | 8 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.128x1024 | 1024GB | 25Gbps | 128 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.16x128 | 128GB | 24Gbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.2x16 | 16GB | 4Gbps | 2 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | N/A|
| mx2.32x256 | 256GB | 25Gbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.48x384 | 384GB | 25Gbps | 48 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.4x32 | 32GB | 8Gbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| mx2.64x512 | 512GB | 25Gbps | 64 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.8x64 | 64GB | 16Gbps | 8 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
{: caption="Table 1. Worker node flavors for Australia." caption-side="bottom"}



## `br-sao`
{: #br-sao}

| Name | Memory | Network speed | Cores | Type | OS | Primary storage | Secondary storage | Secondary storage options |
| -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- |
| bx2.16x64 | 64GB | 24Gbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.2x8 | 8GB | 4Gbps | 2 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | N/A|
| bx2.32x128 | 128GB | 25Gbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.48x192 | 192GB | 25Gbps | 48 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.4x16 | 16GB | 8Gbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| bx2.8x32 | 32GB | 16Gbps | 8 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.16x32 | 32GB | 24Gbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.2x4 | 4GB | 4Gbps | 2 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | N/A|
| cx2.32x64 | 64GB | 25Gbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.48x96 | 96GB | 25Gbps | 48 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.4x8 | 8GB | 8Gbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| cx2.8x16 | 16GB | 16Gbps | 8 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.128x1024 | 1024GB | 25Gbps | 128 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.16x128 | 128GB | 24Gbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.2x16 | 16GB | 4Gbps | 2 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | N/A|
| mx2.32x256 | 256GB | 25Gbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.48x384 | 384GB | 25Gbps | 48 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.4x32 | 32GB | 8Gbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| mx2.64x512 | 512GB | 25Gbps | 64 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.8x64 | 64GB | 16Gbps | 8 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
{: caption="Table 2. Worker node flavors for Brazil." caption-side="bottom"}



## `ca-tor`
{: #ca-tor}

| Name | Memory | Network speed | Cores | Type | OS | Primary storage | Secondary storage | Secondary storage options |
| -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- |
| bx2.16x64 | 64GB | 24Gbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.2x8 | 8GB | 4Gbps | 2 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | N/A|
| bx2.32x128 | 128GB | 25Gbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.48x192 | 192GB | 25Gbps | 48 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.4x16 | 16GB | 8Gbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| bx2.8x32 | 32GB | 16Gbps | 8 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.16x32 | 32GB | 24Gbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.2x4 | 4GB | 4Gbps | 2 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | N/A|
| cx2.32x64 | 64GB | 25Gbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.48x96 | 96GB | 25Gbps | 48 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.4x8 | 8GB | 8Gbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| cx2.8x16 | 16GB | 16Gbps | 8 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.128x1024 | 1024GB | 25Gbps | 128 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.16x128 | 128GB | 24Gbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.2x16 | 16GB | 4Gbps | 2 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | N/A|
| mx2.32x256 | 256GB | 25Gbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.48x384 | 384GB | 25Gbps | 48 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.4x32 | 32GB | 8Gbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| mx2.64x512 | 512GB | 25Gbps | 64 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.8x64 | 64GB | 16Gbps | 8 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
{: caption="Table 3. Worker node flavors for Canada." caption-side="bottom"}



## `eu-de`
{: #eu-de}

| Name | Memory | Network speed | Cores | Type | OS | Primary storage | Secondary storage | Secondary storage options |
| -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- |
| bx2.16x64 | 64GB | 24Gbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.2x8 | 8GB | 4Gbps | 2 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | N/A|
| bx2.32x128 | 128GB | 25Gbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.48x192 | 192GB | 25Gbps | 48 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.4x16 | 16GB | 8Gbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| bx2.8x32 | 32GB | 16Gbps | 8 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.16x32 | 32GB | 24Gbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.2x4 | 4GB | 4Gbps | 2 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | N/A|
| cx2.32x64 | 64GB | 25Gbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.48x96 | 96GB | 25Gbps | 48 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.4x8 | 8GB | 8Gbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| cx2.8x16 | 16GB | 16Gbps | 8 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.128x1024 | 1024GB | 25Gbps | 128 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.16x128 | 128GB | 24Gbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.2x16 | 16GB | 4Gbps | 2 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | N/A|
| mx2.32x256 | 256GB | 25Gbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.48x384 | 384GB | 25Gbps | 48 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.4x32 | 32GB | 8Gbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| mx2.64x512 | 512GB | 25Gbps | 64 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.8x64 | 64GB | 16Gbps | 8 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
{: caption="Table 4. Worker node flavors for Europe." caption-side="bottom"}



## `eu-gb`
{: #eu-gb}

| Name | Memory | Network speed | Cores | Type | OS | Primary storage | Secondary storage | Secondary storage options |
| -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- |
| bx2.16x64 | 64GB | 24Gbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.2x8 | 8GB | 4Gbps | 2 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | N/A|
| bx2.32x128 | 128GB | 25Gbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.48x192 | 192GB | 25Gbps | 48 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.4x16 | 16GB | 8Gbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| bx2.8x32 | 32GB | 16Gbps | 8 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.16x32 | 32GB | 24Gbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.2x4 | 4GB | 4Gbps | 2 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | N/A|
| cx2.32x64 | 64GB | 25Gbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.48x96 | 96GB | 25Gbps | 48 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.4x8 | 8GB | 8Gbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| cx2.8x16 | 16GB | 16Gbps | 8 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.128x1024 | 1024GB | 25Gbps | 128 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.16x128 | 128GB | 24Gbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.2x16 | 16GB | 4Gbps | 2 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | N/A|
| mx2.32x256 | 256GB | 25Gbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.48x384 | 384GB | 25Gbps | 48 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.4x32 | 32GB | 8Gbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| mx2.64x512 | 512GB | 25Gbps | 64 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.8x64 | 64GB | 16Gbps | 8 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
{: caption="Table 5. Worker node flavors for Europe." caption-side="bottom"}



## `jp-osa`
{: #jp-osa}

| Name | Memory | Network speed | Cores | Type | OS | Primary storage | Secondary storage | Secondary storage options |
| -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- |
| bx2.16x64 | 64GB | 24Gbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.2x8 | 8GB | 4Gbps | 2 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | N/A|
| bx2.32x128 | 128GB | 25Gbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.48x192 | 192GB | 25Gbps | 48 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.4x16 | 16GB | 8Gbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| bx2.8x32 | 32GB | 16Gbps | 8 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.16x32 | 32GB | 24Gbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.2x4 | 4GB | 4Gbps | 2 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | N/A|
| cx2.32x64 | 64GB | 25Gbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.48x96 | 96GB | 25Gbps | 48 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.4x8 | 8GB | 8Gbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| cx2.8x16 | 16GB | 16Gbps | 8 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.128x1024 | 1024GB | 25Gbps | 128 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.16x128 | 128GB | 24Gbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.2x16 | 16GB | 4Gbps | 2 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | N/A|
| mx2.32x256 | 256GB | 25Gbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.48x384 | 384GB | 25Gbps | 48 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.4x32 | 32GB | 8Gbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| mx2.64x512 | 512GB | 25Gbps | 64 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.8x64 | 64GB | 16Gbps | 8 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
{: caption="Table 6. Worker node flavors for Japan." caption-side="bottom"}



## `jp-tok`
{: #jp-tok}

| Name | Memory | Network speed | Cores | Type | OS | Primary storage | Secondary storage | Secondary storage options |
| -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- |
| bx2.16x64 | 64GB | 24Gbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.2x8 | 8GB | 4Gbps | 2 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | N/A|
| bx2.32x128 | 128GB | 25Gbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.48x192 | 192GB | 25Gbps | 48 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.4x16 | 16GB | 8Gbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| bx2.8x32 | 32GB | 16Gbps | 8 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.16x32 | 32GB | 24Gbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.2x4 | 4GB | 4Gbps | 2 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | N/A|
| cx2.32x64 | 64GB | 25Gbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.48x96 | 96GB | 25Gbps | 48 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.4x8 | 8GB | 8Gbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| cx2.8x16 | 16GB | 16Gbps | 8 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.128x1024 | 1024GB | 25Gbps | 128 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.16x128 | 128GB | 24Gbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.2x16 | 16GB | 4Gbps | 2 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | N/A|
| mx2.32x256 | 256GB | 25Gbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.48x384 | 384GB | 25Gbps | 48 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.4x32 | 32GB | 8Gbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| mx2.64x512 | 512GB | 25Gbps | 64 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.8x64 | 64GB | 16Gbps | 8 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
{: caption="Table 7. Worker node flavors for Japan." caption-side="bottom"}



## `us-east`
{: #us-east}

| Name | Memory | Network speed | Cores | Type | OS | Primary storage | Secondary storage | Secondary storage options |
| -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- |
| bx2.16x64 | 64GB | 24Gbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.2x8 | 8GB | 4Gbps | 2 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | N/A|
| bx2.32x128 | 128GB | 25Gbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.48x192 | 192GB | 25Gbps | 48 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.4x16 | 16GB | 8Gbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| bx2.8x32 | 32GB | 16Gbps | 8 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.16x32 | 32GB | 24Gbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.2x4 | 4GB | 4Gbps | 2 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | N/A|
| cx2.32x64 | 64GB | 25Gbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.48x96 | 96GB | 25Gbps | 48 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.4x8 | 8GB | 8Gbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| cx2.8x16 | 16GB | 16Gbps | 8 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.128x1024 | 1024GB | 25Gbps | 128 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.16x128 | 128GB | 24Gbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.2x16 | 16GB | 4Gbps | 2 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | N/A|
| mx2.32x256 | 256GB | 25Gbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.48x384 | 384GB | 25Gbps | 48 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.4x32 | 32GB | 8Gbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| mx2.64x512 | 512GB | 25Gbps | 64 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.8x64 | 64GB | 16Gbps | 8 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
{: caption="Table 8. Worker node flavors for United States." caption-side="bottom"}



## `us-south`
{: #us-south}

| Name | Memory | Network speed | Cores | Type | OS | Primary storage | Secondary storage | Secondary storage options |
| -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- | -------------- |
| bx2.16x64 | 64GB | 24Gbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.2x8 | 8GB | 4Gbps | 2 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | N/A|
| bx2.32x128 | 128GB | 25Gbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.48x192 | 192GB | 25Gbps | 48 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| bx2.4x16 | 16GB | 8Gbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| bx2.8x32 | 32GB | 16Gbps | 8 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.16x32 | 32GB | 24Gbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.2x4 | 4GB | 4Gbps | 2 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | N/A|
| cx2.32x64 | 64GB | 25Gbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.48x96 | 96GB | 25Gbps | 48 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| cx2.4x8 | 8GB | 8Gbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| cx2.8x16 | 16GB | 16Gbps | 8 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.128x1024 | 1024GB | 25Gbps | 128 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.16x128 | 128GB | 24Gbps | 16 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.2x16 | 16GB | 4Gbps | 2 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | N/A|
| mx2.32x256 | 256GB | 25Gbps | 32 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.48x384 | 384GB | 25Gbps | 48 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.4x32 | 32GB | 8Gbps | 4 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier |
| mx2.64x512 | 512GB | 25Gbps | 64 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
| mx2.8x64 | 64GB | 16Gbps | 8 | Virtual | **REDHAT_7_64 (default)**, REDHAT_8_64| 100GB BLOCK | N/A | 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |
{: caption="Table 9. Worker node flavors for United States." caption-side="bottom"}




