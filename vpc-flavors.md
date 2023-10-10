---

copyright: 
  years: 2014, 2023
lastupdated: "2023-10-10"

keywords: openshift, node scaling, ca, autoscaler

subcollection: openshift


---



{{site.data.keyword.attribute-definition-list}}



# VPC flavors
{: #vpc-flavors}

Review the VPC Gen 2 worker node flavors by metro.

If your account is allowlisted for flavors that are not listed below, you can find a list of available flavors by running **`ibmcloud oc flavor ls`** [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_flavor_ls).
{: tip}





## `au-syd`
{: #au-syd}

### Australia flavors
{: #au-syd-balanced}

Review the attributes for the Balanced worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| bx2.16x64 | 16, 64GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.2x8 | 2, 8GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A| N/A|
| bx2.32x128 | 32, 128GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.48x192 | 48, 192GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.4x16 | 4, 16GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier | N/A|
| bx2.8x32 | 8, 32GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Balanced flavors in Australia." caption-side="bottom"}
{: #au-syd-balanced-table}
{: tab-title="Balanced profiles"}
{: tab-group="au-syd-tables"}


### Australia flavors
{: #au-syd-compute}

Review the attributes for the Compute worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| cx2.16x32 | 16, 32GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.2x4 | 2, 4GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A| N/A|
| cx2.32x64 | 32, 64GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.48x96 | 48, 96GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.4x8 | 4, 8GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier | N/A|
| cx2.8x16 | 8, 16GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Compute flavors in Australia." caption-side="bottom"}
{: #au-syd-compute-table}
{: tab-title="Compute profiles"}
{: tab-group="au-syd-tables"}



### Australia flavors
{: #au-syd-memory}

Review the attributes for the Memory worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| mx2.128x1024 | 128, 1024GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.16x128 | 16, 128GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.16x128.2000gb | 16, 128GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | 2000GB BLOCK | N/A| N/A|
| mx2.2x16 | 2, 16GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A| N/A|
| mx2.32x256 | 32, 256GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.48x384 | 48, 384GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.4x32 | 4, 32GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier | N/A|
| mx2.64x512 | 64, 512GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.8x64 | 8, 64GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Memory flavors in Australia." caption-side="bottom"}
{: #au-syd-memory-table}
{: tab-title="Memory profiles"}
{: tab-group="au-syd-tables"}







## `br-sao`
{: #br-sao}

### Brazil flavors
{: #br-sao-balanced}

Review the attributes for the Balanced worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| bx2.16x64 | 16, 64GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.2x8 | 2, 8GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A| N/A|
| bx2.32x128 | 32, 128GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.48x192 | 48, 192GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.4x16 | 4, 16GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier | N/A|
| bx2.8x32 | 8, 32GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Balanced flavors in Brazil." caption-side="bottom"}
{: #br-sao-balanced-table}
{: tab-title="Balanced profiles"}
{: tab-group="br-sao-tables"}


### Brazil flavors
{: #br-sao-compute}

Review the attributes for the Compute worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| cx2.16x32 | 16, 32GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.2x4 | 2, 4GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A| N/A|
| cx2.32x64 | 32, 64GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.48x96 | 48, 96GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.4x8 | 4, 8GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier | N/A|
| cx2.8x16 | 8, 16GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Compute flavors in Brazil." caption-side="bottom"}
{: #br-sao-compute-table}
{: tab-title="Compute profiles"}
{: tab-group="br-sao-tables"}



### Brazil flavors
{: #br-sao-memory}

Review the attributes for the Memory worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| mx2.128x1024 | 128, 1024GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.16x128 | 16, 128GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.2x16 | 2, 16GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A| N/A|
| mx2.32x256 | 32, 256GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.48x384 | 48, 384GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.4x32 | 4, 32GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier | N/A|
| mx2.64x512 | 64, 512GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.8x64 | 8, 64GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Memory flavors in Brazil." caption-side="bottom"}
{: #br-sao-memory-table}
{: tab-title="Memory profiles"}
{: tab-group="br-sao-tables"}







## `ca-tor`
{: #ca-tor}

### Canada flavors
{: #ca-tor-balanced}

Review the attributes for the Balanced worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| bx2.16x64 | 16, 64GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.2x8 | 2, 8GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A| N/A|
| bx2.32x128 | 32, 128GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.48x192 | 48, 192GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.4x16 | 4, 16GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier | N/A|
| bx2.8x32 | 8, 32GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Balanced flavors in Canada." caption-side="bottom"}
{: #ca-tor-balanced-table}
{: tab-title="Balanced profiles"}
{: tab-group="ca-tor-tables"}


### Canada flavors
{: #ca-tor-compute}

Review the attributes for the Compute worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| cx2.16x32 | 16, 32GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.2x4 | 2, 4GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A| N/A|
| cx2.32x64 | 32, 64GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.48x96 | 48, 96GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.4x8 | 4, 8GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier | N/A|
| cx2.8x16 | 8, 16GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Compute flavors in Canada." caption-side="bottom"}
{: #ca-tor-compute-table}
{: tab-title="Compute profiles"}
{: tab-group="ca-tor-tables"}



### Canada flavors
{: #ca-tor-memory}

Review the attributes for the Memory worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| mx2.128x1024 | 128, 1024GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.16x128 | 16, 128GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.16x128.2000gb | 16, 128GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | 2000GB BLOCK | N/A| N/A|
| mx2.2x16 | 2, 16GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A| N/A|
| mx2.32x256 | 32, 256GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.48x384 | 48, 384GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.4x32 | 4, 32GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier | N/A|
| mx2.64x512 | 64, 512GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.8x64 | 8, 64GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Memory flavors in Canada." caption-side="bottom"}
{: #ca-tor-memory-table}
{: tab-title="Memory profiles"}
{: tab-group="ca-tor-tables"}







## `eu-de`
{: #eu-de}

### Europe flavors
{: #eu-de-balanced}

Review the attributes for the Balanced worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| bx2.16x64 | 16, 64GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.2x8 | 2, 8GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A| N/A|
| bx2.32x128 | 32, 128GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.48x192 | 48, 192GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.4x16 | 4, 16GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier | N/A|
| bx2.8x32 | 8, 32GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Balanced flavors in Europe." caption-side="bottom"}
{: #eu-de-balanced-table}
{: tab-title="Balanced profiles"}
{: tab-group="eu-de-tables"}


### Europe flavors
{: #eu-de-compute}

Review the attributes for the Compute worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| cx2.16x32 | 16, 32GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.2x4 | 2, 4GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A| N/A|
| cx2.32x64 | 32, 64GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.48x96 | 48, 96GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.4x8 | 4, 8GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier | N/A|
| cx2.8x16 | 8, 16GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Compute flavors in Europe." caption-side="bottom"}
{: #eu-de-compute-table}
{: tab-title="Compute profiles"}
{: tab-group="eu-de-tables"}



### Europe flavors
{: #eu-de-memory}

Review the attributes for the Memory worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| mx2.128x1024 | 128, 1024GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.16x128 | 16, 128GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.16x128.2000gb | 16, 128GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | 2000GB BLOCK | N/A| N/A|
| mx2.2x16 | 2, 16GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A| N/A|
| mx2.32x256 | 32, 256GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.48x384 | 48, 384GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.4x32 | 4, 32GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier | N/A|
| mx2.64x512 | 64, 512GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.8x64 | 8, 64GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Memory flavors in Europe." caption-side="bottom"}
{: #eu-de-memory-table}
{: tab-title="Memory profiles"}
{: tab-group="eu-de-tables"}







## `eu-es`
{: #eu-es}

### Europe flavors
{: #eu-es-balanced}

Review the attributes for the Balanced worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| bx2.16x64 | 16, 64GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.2x8 | 2, 8GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A| N/A|
| bx2.32x128 | 32, 128GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.48x192 | 48, 192GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.4x16 | 4, 16GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier | N/A|
| bx2.8x32 | 8, 32GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Balanced flavors in Europe." caption-side="bottom"}
{: #eu-es-balanced-table}
{: tab-title="Balanced profiles"}
{: tab-group="eu-es-tables"}


### Europe flavors
{: #eu-es-compute}

Review the attributes for the Compute worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| cx2.16x32 | 16, 32GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.2x4 | 2, 4GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A| N/A|
| cx2.32x64 | 32, 64GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.48x96 | 48, 96GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.4x8 | 4, 8GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier | N/A|
| cx2.8x16 | 8, 16GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Compute flavors in Europe." caption-side="bottom"}
{: #eu-es-compute-table}
{: tab-title="Compute profiles"}
{: tab-group="eu-es-tables"}



### Europe flavors
{: #eu-es-memory}

Review the attributes for the Memory worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| mx2.128x1024 | 128, 1024GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.16x128 | 16, 128GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.2x16 | 2, 16GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A| N/A|
| mx2.32x256 | 32, 256GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.48x384 | 48, 384GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.4x32 | 4, 32GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier | N/A|
| mx2.64x512 | 64, 512GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.8x64 | 8, 64GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Memory flavors in Europe." caption-side="bottom"}
{: #eu-es-memory-table}
{: tab-title="Memory profiles"}
{: tab-group="eu-es-tables"}







## `eu-gb`
{: #eu-gb}

### Europe flavors
{: #eu-gb-balanced}

Review the attributes for the Balanced worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| bx2.16x64 | 16, 64GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.2x8 | 2, 8GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A| N/A|
| bx2.32x128 | 32, 128GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.48x192 | 48, 192GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.4x16 | 4, 16GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier | N/A|
| bx2.8x32 | 8, 32GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Balanced flavors in Europe." caption-side="bottom"}
{: #eu-gb-balanced-table}
{: tab-title="Balanced profiles"}
{: tab-group="eu-gb-tables"}


### Europe flavors
{: #eu-gb-compute}

Review the attributes for the Compute worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| cx2.16x32 | 16, 32GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.2x4 | 2, 4GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A| N/A|
| cx2.32x64 | 32, 64GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.48x96 | 48, 96GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.4x8 | 4, 8GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier | N/A|
| cx2.8x16 | 8, 16GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Compute flavors in Europe." caption-side="bottom"}
{: #eu-gb-compute-table}
{: tab-title="Compute profiles"}
{: tab-group="eu-gb-tables"}



### Europe flavors
{: #eu-gb-memory}

Review the attributes for the Memory worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| mx2.128x1024 | 128, 1024GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.16x128 | 16, 128GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.16x128.2000gb | 16, 128GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | 2000GB BLOCK | N/A| N/A|
| mx2.2x16 | 2, 16GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A| N/A|
| mx2.32x256 | 32, 256GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.48x384 | 48, 384GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.4x32 | 4, 32GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier | N/A|
| mx2.64x512 | 64, 512GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.8x64 | 8, 64GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Memory flavors in Europe." caption-side="bottom"}
{: #eu-gb-memory-table}
{: tab-title="Memory profiles"}
{: tab-group="eu-gb-tables"}







## `jp-osa`
{: #jp-osa}

### Japan flavors
{: #jp-osa-balanced}

Review the attributes for the Balanced worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| bx2.16x64 | 16, 64GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.2x8 | 2, 8GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A| N/A|
| bx2.32x128 | 32, 128GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.48x192 | 48, 192GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.4x16 | 4, 16GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier | N/A|
| bx2.8x32 | 8, 32GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Balanced flavors in Japan." caption-side="bottom"}
{: #jp-osa-balanced-table}
{: tab-title="Balanced profiles"}
{: tab-group="jp-osa-tables"}


### Japan flavors
{: #jp-osa-compute}

Review the attributes for the Compute worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| cx2.16x32 | 16, 32GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.2x4 | 2, 4GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A| N/A|
| cx2.32x64 | 32, 64GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.48x96 | 48, 96GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.4x8 | 4, 8GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier | N/A|
| cx2.8x16 | 8, 16GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Compute flavors in Japan." caption-side="bottom"}
{: #jp-osa-compute-table}
{: tab-title="Compute profiles"}
{: tab-group="jp-osa-tables"}



### Japan flavors
{: #jp-osa-memory}

Review the attributes for the Memory worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| mx2.128x1024 | 128, 1024GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.16x128 | 16, 128GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.2x16 | 2, 16GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A| N/A|
| mx2.32x256 | 32, 256GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.48x384 | 48, 384GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.4x32 | 4, 32GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier | N/A|
| mx2.64x512 | 64, 512GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.8x64 | 8, 64GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Memory flavors in Japan." caption-side="bottom"}
{: #jp-osa-memory-table}
{: tab-title="Memory profiles"}
{: tab-group="jp-osa-tables"}







## `jp-tok`
{: #jp-tok}

### Japan flavors
{: #jp-tok-balanced}

Review the attributes for the Balanced worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| bx2.16x64 | 16, 64GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.2x8 | 2, 8GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A| N/A|
| bx2.32x128 | 32, 128GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.48x192 | 48, 192GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.4x16 | 4, 16GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier | N/A|
| bx2.8x32 | 8, 32GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Balanced flavors in Japan." caption-side="bottom"}
{: #jp-tok-balanced-table}
{: tab-title="Balanced profiles"}
{: tab-group="jp-tok-tables"}


### Japan flavors
{: #jp-tok-compute}

Review the attributes for the Compute worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| cx2.16x32 | 16, 32GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.2x4 | 2, 4GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A| N/A|
| cx2.32x64 | 32, 64GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.48x96 | 48, 96GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.4x8 | 4, 8GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier | N/A|
| cx2.8x16 | 8, 16GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Compute flavors in Japan." caption-side="bottom"}
{: #jp-tok-compute-table}
{: tab-title="Compute profiles"}
{: tab-group="jp-tok-tables"}



### Japan flavors
{: #jp-tok-memory}

Review the attributes for the Memory worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| mx2.128x1024 | 128, 1024GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.16x128 | 16, 128GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.16x128.2000gb | 16, 128GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | 2000GB BLOCK | N/A| N/A|
| mx2.2x16 | 2, 16GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A| N/A|
| mx2.32x256 | 32, 256GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.48x384 | 48, 384GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.4x32 | 4, 32GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier | N/A|
| mx2.64x512 | 64, 512GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.8x64 | 8, 64GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Memory flavors in Japan." caption-side="bottom"}
{: #jp-tok-memory-table}
{: tab-title="Memory profiles"}
{: tab-group="jp-tok-tables"}







## `us-east`
{: #us-east}

### United States flavors
{: #us-east-balanced}

Review the attributes for the Balanced worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| bx2.16x64 | 16, 64GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.2x8 | 2, 8GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A| N/A|
| bx2.32x128 | 32, 128GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.48x192 | 48, 192GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.4x16 | 4, 16GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier | N/A|
| bx2.8x32 | 8, 32GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Balanced flavors in United States." caption-side="bottom"}
{: #us-east-balanced-table}
{: tab-title="Balanced profiles"}
{: tab-group="us-east-tables"}


### United States flavors
{: #us-east-compute}

Review the attributes for the Compute worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| cx2.16x32 | 16, 32GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.2x4 | 2, 4GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A| N/A|
| cx2.32x64 | 32, 64GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.48x96 | 48, 96GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.4x8 | 4, 8GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier | N/A|
| cx2.8x16 | 8, 16GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Compute flavors in United States." caption-side="bottom"}
{: #us-east-compute-table}
{: tab-title="Compute profiles"}
{: tab-group="us-east-tables"}



### United States flavors
{: #us-east-memory}

Review the attributes for the Memory worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| mx2.128x1024 | 128, 1024GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.16x128 | 16, 128GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.16x128.2000gb | 16, 128GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | 2000GB BLOCK | N/A| N/A|
| mx2.2x16 | 2, 16GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A| N/A|
| mx2.32x256 | 32, 256GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.48x384 | 48, 384GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.4x32 | 4, 32GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier | N/A|
| mx2.64x512 | 64, 512GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.8x64 | 8, 64GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Memory flavors in United States." caption-side="bottom"}
{: #us-east-memory-table}
{: tab-title="Memory profiles"}
{: tab-group="us-east-tables"}







## `us-south`
{: #us-south}

### United States flavors
{: #us-south-balanced}

Review the attributes for the Balanced worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| bx2.16x64 | 16, 64GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.2x8 | 2, 8GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A| N/A|
| bx2.32x128 | 32, 128GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.48x192 | 48, 192GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.4x16 | 4, 16GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier | N/A|
| bx2.8x32 | 8, 32GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Balanced flavors in United States." caption-side="bottom"}
{: #us-south-balanced-table}
{: tab-title="Balanced profiles"}
{: tab-group="us-south-tables"}


### United States flavors
{: #us-south-compute}

Review the attributes for the Compute worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| cx2.16x32 | 16, 32GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.2x4 | 2, 4GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A| N/A|
| cx2.32x64 | 32, 64GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.48x96 | 48, 96GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.4x8 | 4, 8GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier | N/A|
| cx2.8x16 | 8, 16GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Compute flavors in United States." caption-side="bottom"}
{: #us-south-compute-table}
{: tab-title="Compute profiles"}
{: tab-group="us-south-tables"}



### United States flavors
{: #us-south-memory}

Review the attributes for the Memory worker node flavors.

| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| mx2.128x1024 | 128, 1024GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.16x128 | 16, 128GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.16x128.2000gb | 16, 128GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | 2000GB BLOCK | N/A| N/A|
| mx2.2x16 | 2, 16GB, 4Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | N/A| N/A|
| mx2.32x256 | 32, 256GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.48x384 | 48, 384GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.4x32 | 4, 32GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier | N/A|
| mx2.64x512 | 64, 512GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.8x64 | 8, 64GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 600gb.5iops-tier, 900gb.5iops-tier, 1200gb.5iops-tier, 1600gb.5iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Memory flavors in United States." caption-side="bottom"}
{: #us-south-memory-table}
{: tab-title="Memory profiles"}
{: tab-group="us-south-tables"}








