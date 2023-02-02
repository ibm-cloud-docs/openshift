---

copyright: 
  years: 2014, 2023
lastupdated: "2023-02-02"

keywords: openshift, node scaling, ca, autoscaler

subcollection: openshift


---



{{site.data.keyword.attribute-definition-list}}



# VPC flavors
{: #vpc-flavors}

Review the VPC Gen 2 worker node flavors by zone.









## au-syd-1
{: #au-syd-1}

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
{: caption="Table 1. Worker node flavors for au-syd-1" caption-side="bottom"}

## au-syd-2
{: #au-syd-2}

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
{: caption="Table 2. Worker node flavors for au-syd-2" caption-side="bottom"}

## au-syd-3
{: #au-syd-3}

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
{: caption="Table 3. Worker node flavors for au-syd-3" caption-side="bottom"}

## br-sao-1
{: #br-sao-1}

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
{: caption="Table 4. Worker node flavors for br-sao-1" caption-side="bottom"}

## br-sao-2
{: #br-sao-2}

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
{: caption="Table 5. Worker node flavors for br-sao-2" caption-side="bottom"}

## br-sao-3
{: #br-sao-3}

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
{: caption="Table 6. Worker node flavors for br-sao-3" caption-side="bottom"}

## ca-tor-1
{: #ca-tor-1}

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
{: caption="Table 7. Worker node flavors for ca-tor-1" caption-side="bottom"}

## ca-tor-2
{: #ca-tor-2}

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
{: caption="Table 8. Worker node flavors for ca-tor-2" caption-side="bottom"}

## ca-tor-3
{: #ca-tor-3}

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
{: caption="Table 9. Worker node flavors for ca-tor-3" caption-side="bottom"}

## eu-de-1
{: #eu-de-1}

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
{: caption="Table 10. Worker node flavors for eu-de-1" caption-side="bottom"}

## eu-de-2
{: #eu-de-2}

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
{: caption="Table 11. Worker node flavors for eu-de-2" caption-side="bottom"}

## eu-de-3
{: #eu-de-3}

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
{: caption="Table 12. Worker node flavors for eu-de-3" caption-side="bottom"}

## eu-gb-1
{: #eu-gb-1}

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
{: caption="Table 13. Worker node flavors for eu-gb-1" caption-side="bottom"}

## eu-gb-2
{: #eu-gb-2}

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
{: caption="Table 14. Worker node flavors for eu-gb-2" caption-side="bottom"}

## eu-gb-3
{: #eu-gb-3}

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
{: caption="Table 15. Worker node flavors for eu-gb-3" caption-side="bottom"}

## jp-osa-1
{: #jp-osa-1}

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
{: caption="Table 16. Worker node flavors for jp-osa-1" caption-side="bottom"}

## jp-osa-2
{: #jp-osa-2}

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
{: caption="Table 17. Worker node flavors for jp-osa-2" caption-side="bottom"}

## jp-osa-3
{: #jp-osa-3}

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
{: caption="Table 18. Worker node flavors for jp-osa-3" caption-side="bottom"}

## jp-tok-1
{: #jp-tok-1}

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
{: caption="Table 19. Worker node flavors for jp-tok-1" caption-side="bottom"}

## jp-tok-2
{: #jp-tok-2}

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
{: caption="Table 20. Worker node flavors for jp-tok-2" caption-side="bottom"}

## jp-tok-3
{: #jp-tok-3}

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
{: caption="Table 21. Worker node flavors for jp-tok-3" caption-side="bottom"}

## us-east-1
{: #us-east-1}

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
{: caption="Table 22. Worker node flavors for us-east-1" caption-side="bottom"}

## us-east-2
{: #us-east-2}

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
{: caption="Table 23. Worker node flavors for us-east-2" caption-side="bottom"}

## us-east-3
{: #us-east-3}

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
{: caption="Table 24. Worker node flavors for us-east-3" caption-side="bottom"}

## us-south-1
{: #us-south-1}

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
{: caption="Table 25. Worker node flavors for us-south-1" caption-side="bottom"}

## us-south-2
{: #us-south-2}

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
{: caption="Table 26. Worker node flavors for us-south-2" caption-side="bottom"}

## us-south-3
{: #us-south-3}

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
{: caption="Table 27. Worker node flavors for us-south-3" caption-side="bottom"}


