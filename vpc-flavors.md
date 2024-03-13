---

copyright: 
  years: 2014, 2024
lastupdated: "2024-03-13"


keywords: openshift, node scaling, ca, autoscaler

subcollection: openshift


---



{{site.data.keyword.attribute-definition-list}}



# VPC flavors
{: #vpc-flavors}

Review the VPC Gen 2 worker node flavors by metro.

Additional flavor types, including flavors with NVIDIA V100 GPUs are available for allowlisted accounts only. To request access to other allowlisted flavors, [request access to the allowlist](/docs/openshift?topic=openshift-allowlist-request).
{: note}

If your account is allowlisted for flavors that are not listed below, you can find a list of available flavors by running **`ibmcloud oc flavor ls`** [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_flavor_ls).




## Sydney (`au-syd`)
{: #sydney-au-syd}



| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| bx2.16x64 | 16, 64GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.32x128 | 32, 128GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.48x192 | 48, 192GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.4x16 | 4, 16GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier | N/A|
| bx2.8x32 | 8, 32GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Balanced flavors in Sydney." caption-side="bottom"}
{: #au-syd-balanced-table}
{: tab-title="Balanced"}
{: tab-group="au-syd-tables"}


| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| cx2.16x32 | 16, 32GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.32x64 | 32, 64GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.48x96 | 48, 96GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.8x16 | 8, 16GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Compute flavors in Sydney." caption-side="bottom"}
{: #au-syd-compute-table}
{: tab-title="Compute"}
{: tab-group="au-syd-tables"}


| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| gx3.16x80.l4 | 16, 80GB, 32Gbps | Virtual | **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |1 L4 |
| gx3.32x160.2l4 | 32, 160GB, 32Gbps | Virtual | **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |2 L4 |
| gx3.64x320.4l4 | 64, 320GB, 32Gbps | Virtual | **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |4 L4 |
{: class="simple-tab-table"}
{: caption="Table. GPU flavors in Sydney." caption-side="bottom"}
{: #au-syd-gpu-table}
{: tab-title="GPU"}
{: tab-group="au-syd-tables"}


| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| mx2.128x1024 | 128, 1024GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.16x128 | 16, 128GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.16x128.2000gb | 16, 128GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | 2000GB BLOCK | N/A| N/A|
| mx2.32x256 | 32, 256GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.48x384 | 48, 384GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.4x32 | 4, 32GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier | N/A|
| mx2.64x512 | 64, 512GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.8x64 | 8, 64GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Memory flavors in Sydney." caption-side="bottom"}
{: #au-syd-memory-table}
{: tab-title="Memory"}
{: tab-group="au-syd-tables"}




## Sao Paulo (`br-sao`)
{: #sao-paulo-br-sao}



| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| bx2.16x64 | 16, 64GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.32x128 | 32, 128GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.48x192 | 48, 192GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.4x16 | 4, 16GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier | N/A|
| bx2.8x32 | 8, 32GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Balanced flavors in Sao Paulo." caption-side="bottom"}
{: #br-sao-balanced-table}
{: tab-title="Balanced"}
{: tab-group="br-sao-tables"}


| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| cx2.16x32 | 16, 32GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.32x64 | 32, 64GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.48x96 | 48, 96GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.8x16 | 8, 16GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Compute flavors in Sao Paulo." caption-side="bottom"}
{: #br-sao-compute-table}
{: tab-title="Compute"}
{: tab-group="br-sao-tables"}



| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| mx2.128x1024 | 128, 1024GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.16x128 | 16, 128GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.32x256 | 32, 256GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.48x384 | 48, 384GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.4x32 | 4, 32GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier | N/A|
| mx2.64x512 | 64, 512GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.8x64 | 8, 64GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Memory flavors in Sao Paulo." caption-side="bottom"}
{: #br-sao-memory-table}
{: tab-title="Memory"}
{: tab-group="br-sao-tables"}




## Toronto (`ca-tor`)
{: #toronto-ca-tor}



| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| bx2.16x64 | 16, 64GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.32x128 | 32, 128GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.48x192 | 48, 192GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.4x16 | 4, 16GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier | N/A|
| bx2.8x32 | 8, 32GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Balanced flavors in Toronto." caption-side="bottom"}
{: #ca-tor-balanced-table}
{: tab-title="Balanced"}
{: tab-group="ca-tor-tables"}


| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| cx2.16x32 | 16, 32GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.32x64 | 32, 64GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.48x96 | 48, 96GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.8x16 | 8, 16GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Compute flavors in Toronto." caption-side="bottom"}
{: #ca-tor-compute-table}
{: tab-title="Compute"}
{: tab-group="ca-tor-tables"}


| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| gx3.16x80.l4 | 16, 80GB, 32Gbps | Virtual | **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |1 L4 |
| gx3.32x160.2l4 | 32, 160GB, 32Gbps | Virtual | **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |2 L4 |
| gx3.64x320.4l4 | 64, 320GB, 32Gbps | Virtual | **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |4 L4 |
{: class="simple-tab-table"}
{: caption="Table. GPU flavors in Toronto." caption-side="bottom"}
{: #ca-tor-gpu-table}
{: tab-title="GPU"}
{: tab-group="ca-tor-tables"}


| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| mx2.128x1024 | 128, 1024GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.16x128 | 16, 128GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.16x128.2000gb | 16, 128GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | 2000GB BLOCK | N/A| N/A|
| mx2.32x256 | 32, 256GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.48x384 | 48, 384GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.4x32 | 4, 32GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier | N/A|
| mx2.64x512 | 64, 512GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.8x64 | 8, 64GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Memory flavors in Toronto." caption-side="bottom"}
{: #ca-tor-memory-table}
{: tab-title="Memory"}
{: tab-group="ca-tor-tables"}




## Frankfurt (`eu-de`)
{: #frankfurt-eu-de}



| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| bx2.16x64 | 16, 64GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.32x128 | 32, 128GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.48x192 | 48, 192GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.4x16 | 4, 16GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier | N/A|
| bx2.8x32 | 8, 32GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Balanced flavors in Frankfurt." caption-side="bottom"}
{: #eu-de-balanced-table}
{: tab-title="Balanced"}
{: tab-group="eu-de-tables"}


| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| cx2.16x32 | 16, 32GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.32x64 | 32, 64GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.48x96 | 48, 96GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.8x16 | 8, 16GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Compute flavors in Frankfurt." caption-side="bottom"}
{: #eu-de-compute-table}
{: tab-title="Compute"}
{: tab-group="eu-de-tables"}


| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| gx3.16x80.l4 | 16, 80GB, 32Gbps | Virtual | **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |1 L4 |
| gx3.32x160.2l4 | 32, 160GB, 32Gbps | Virtual | **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |2 L4 |
| gx3.64x320.4l4 | 64, 320GB, 32Gbps | Virtual | **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |4 L4 |
{: class="simple-tab-table"}
{: caption="Table. GPU flavors in Frankfurt." caption-side="bottom"}
{: #eu-de-gpu-table}
{: tab-title="GPU"}
{: tab-group="eu-de-tables"}


| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| mx2.128x1024 | 128, 1024GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.16x128 | 16, 128GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.16x128.2000gb | 16, 128GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | 2000GB BLOCK | N/A| N/A|
| mx2.32x256 | 32, 256GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.48x384 | 48, 384GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.4x32 | 4, 32GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier | N/A|
| mx2.64x512 | 64, 512GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.8x64 | 8, 64GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Memory flavors in Frankfurt." caption-side="bottom"}
{: #eu-de-memory-table}
{: tab-title="Memory"}
{: tab-group="eu-de-tables"}




## Madrid (`eu-es`)
{: #madrid-eu-es}



| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| bx2.16x64 | 16, 64GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.32x128 | 32, 128GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.48x192 | 48, 192GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.4x16 | 4, 16GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier | N/A|
| bx2.8x32 | 8, 32GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Balanced flavors in Madrid." caption-side="bottom"}
{: #eu-es-balanced-table}
{: tab-title="Balanced"}
{: tab-group="eu-es-tables"}


| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| cx2.16x32 | 16, 32GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.32x64 | 32, 64GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.48x96 | 48, 96GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.8x16 | 8, 16GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Compute flavors in Madrid." caption-side="bottom"}
{: #eu-es-compute-table}
{: tab-title="Compute"}
{: tab-group="eu-es-tables"}


| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| gx3.16x80.l4 | 16, 80GB, 32Gbps | Virtual | **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |1 L4 |
| gx3.32x160.2l4 | 32, 160GB, 32Gbps | Virtual | **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |2 L4 |
| gx3.64x320.4l4 | 64, 320GB, 32Gbps | Virtual | **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |4 L4 |
{: class="simple-tab-table"}
{: caption="Table. GPU flavors in Madrid." caption-side="bottom"}
{: #eu-es-gpu-table}
{: tab-title="GPU"}
{: tab-group="eu-es-tables"}


| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| mx2.128x1024 | 128, 1024GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.16x128 | 16, 128GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.32x256 | 32, 256GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.48x384 | 48, 384GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.4x32 | 4, 32GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier | N/A|
| mx2.64x512 | 64, 512GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.8x64 | 8, 64GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Memory flavors in Madrid." caption-side="bottom"}
{: #eu-es-memory-table}
{: tab-title="Memory"}
{: tab-group="eu-es-tables"}




## London (`eu-gb`)
{: #london-eu-gb}



| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| bx2.16x64 | 16, 64GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.32x128 | 32, 128GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.48x192 | 48, 192GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.4x16 | 4, 16GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier | N/A|
| bx2.8x32 | 8, 32GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Balanced flavors in London." caption-side="bottom"}
{: #eu-gb-balanced-table}
{: tab-title="Balanced"}
{: tab-group="eu-gb-tables"}


| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| cx2.16x32 | 16, 32GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.32x64 | 32, 64GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.48x96 | 48, 96GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.8x16 | 8, 16GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Compute flavors in London." caption-side="bottom"}
{: #eu-gb-compute-table}
{: tab-title="Compute"}
{: tab-group="eu-gb-tables"}


| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| gx3.16x80.l4 | 16, 80GB, 32Gbps | Virtual | **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |1 L4 |
| gx3.32x160.2l4 | 32, 160GB, 32Gbps | Virtual | **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |2 L4 |
| gx3.64x320.4l4 | 64, 320GB, 32Gbps | Virtual | **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |4 L4 |
{: class="simple-tab-table"}
{: caption="Table. GPU flavors in London." caption-side="bottom"}
{: #eu-gb-gpu-table}
{: tab-title="GPU"}
{: tab-group="eu-gb-tables"}


| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| mx2.128x1024 | 128, 1024GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.16x128 | 16, 128GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.16x128.2000gb | 16, 128GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | 2000GB BLOCK | N/A| N/A|
| mx2.32x256 | 32, 256GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.48x384 | 48, 384GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.4x32 | 4, 32GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier | N/A|
| mx2.64x512 | 64, 512GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.8x64 | 8, 64GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Memory flavors in London." caption-side="bottom"}
{: #eu-gb-memory-table}
{: tab-title="Memory"}
{: tab-group="eu-gb-tables"}




## Osaka (`jp-osa`)
{: #osaka-jp-osa}



| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| bx2.16x64 | 16, 64GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.32x128 | 32, 128GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.48x192 | 48, 192GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.4x16 | 4, 16GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier | N/A|
| bx2.8x32 | 8, 32GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Balanced flavors in Osaka." caption-side="bottom"}
{: #jp-osa-balanced-table}
{: tab-title="Balanced"}
{: tab-group="jp-osa-tables"}


| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| cx2.16x32 | 16, 32GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.32x64 | 32, 64GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.48x96 | 48, 96GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.8x16 | 8, 16GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Compute flavors in Osaka." caption-side="bottom"}
{: #jp-osa-compute-table}
{: tab-title="Compute"}
{: tab-group="jp-osa-tables"}



| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| mx2.128x1024 | 128, 1024GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.16x128 | 16, 128GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.32x256 | 32, 256GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.48x384 | 48, 384GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.4x32 | 4, 32GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier | N/A|
| mx2.64x512 | 64, 512GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.8x64 | 8, 64GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Memory flavors in Osaka." caption-side="bottom"}
{: #jp-osa-memory-table}
{: tab-title="Memory"}
{: tab-group="jp-osa-tables"}




## Tokyo (`jp-tok`)
{: #tokyo-jp-tok}



| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| bx2.16x64 | 16, 64GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.32x128 | 32, 128GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.48x192 | 48, 192GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.4x16 | 4, 16GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier | N/A|
| bx2.8x32 | 8, 32GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Balanced flavors in Tokyo." caption-side="bottom"}
{: #jp-tok-balanced-table}
{: tab-title="Balanced"}
{: tab-group="jp-tok-tables"}


| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| cx2.16x32 | 16, 32GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.32x64 | 32, 64GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.48x96 | 48, 96GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.8x16 | 8, 16GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Compute flavors in Tokyo." caption-side="bottom"}
{: #jp-tok-compute-table}
{: tab-title="Compute"}
{: tab-group="jp-tok-tables"}


| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| gx3.16x80.l4 | 16, 80GB, 32Gbps | Virtual | **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |1 L4 |
| gx3.32x160.2l4 | 32, 160GB, 32Gbps | Virtual | **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |2 L4 |
| gx3.64x320.4l4 | 64, 320GB, 32Gbps | Virtual | **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |4 L4 |
{: class="simple-tab-table"}
{: caption="Table. GPU flavors in Tokyo." caption-side="bottom"}
{: #jp-tok-gpu-table}
{: tab-title="GPU"}
{: tab-group="jp-tok-tables"}


| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| mx2.128x1024 | 128, 1024GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.16x128 | 16, 128GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.16x128.2000gb | 16, 128GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | 2000GB BLOCK | N/A| N/A|
| mx2.32x256 | 32, 256GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.48x384 | 48, 384GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.4x32 | 4, 32GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier | N/A|
| mx2.64x512 | 64, 512GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.8x64 | 8, 64GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Memory flavors in Tokyo." caption-side="bottom"}
{: #jp-tok-memory-table}
{: tab-title="Memory"}
{: tab-group="jp-tok-tables"}




## Washington DC (`us-east`)
{: #washington-dc-us-east}



| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| bx2.16x64 | 16, 64GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.32x128 | 32, 128GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.48x192 | 48, 192GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.4x16 | 4, 16GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier | N/A|
| bx2.8x32 | 8, 32GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Balanced flavors in Washington DC." caption-side="bottom"}
{: #us-east-balanced-table}
{: tab-title="Balanced"}
{: tab-group="us-east-tables"}


| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| cx2.16x32 | 16, 32GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.32x64 | 32, 64GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.48x96 | 48, 96GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.8x16 | 8, 16GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Compute flavors in Washington DC." caption-side="bottom"}
{: #us-east-compute-table}
{: tab-title="Compute"}
{: tab-group="us-east-tables"}


| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| gx3.16x80.l4 | 16, 80GB, 32Gbps | Virtual | **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |1 L4 |
| gx3.32x160.2l4 | 32, 160GB, 32Gbps | Virtual | **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |2 L4 |
| gx3.64x320.4l4 | 64, 320GB, 32Gbps | Virtual | **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier |4 L4 |
{: class="simple-tab-table"}
{: caption="Table. GPU flavors in Washington DC." caption-side="bottom"}
{: #us-east-gpu-table}
{: tab-title="GPU"}
{: tab-group="us-east-tables"}


| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| mx2.128x1024 | 128, 1024GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.16x128 | 16, 128GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.16x128.2000gb | 16, 128GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | 2000GB BLOCK | N/A| N/A|
| mx2.32x256 | 32, 256GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.48x384 | 48, 384GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.4x32 | 4, 32GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier | N/A|
| mx2.64x512 | 64, 512GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.8x64 | 8, 64GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Memory flavors in Washington DC." caption-side="bottom"}
{: #us-east-memory-table}
{: tab-title="Memory"}
{: tab-group="us-east-tables"}




## Dallas (`us-south`)
{: #dallas-us-south}



| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| bx2.16x64 | 16, 64GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.32x128 | 32, 128GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.48x192 | 48, 192GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| bx2.4x16 | 4, 16GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier | N/A|
| bx2.8x32 | 8, 32GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Balanced flavors in Dallas." caption-side="bottom"}
{: #us-south-balanced-table}
{: tab-title="Balanced"}
{: tab-group="us-south-tables"}


| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| cx2.16x32 | 16, 32GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.32x64 | 32, 64GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.48x96 | 48, 96GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| cx2.8x16 | 8, 16GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Compute flavors in Dallas." caption-side="bottom"}
{: #us-south-compute-table}
{: tab-title="Compute"}
{: tab-group="us-south-tables"}



| Name | Cores, Memory, and Network speed | Type | OS | Primary storage | Secondary storage | Secondary storage options | GPUs |
| ---- | -------------------------------- | ---- | -- | --------------- | ----------------- |  -------------- |-- |
| mx2.128x1024 | 128, 1024GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.16x128 | 16, 128GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.16x128.2000gb | 16, 128GB, 24Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | 2000GB BLOCK | N/A| N/A|
| mx2.32x256 | 32, 256GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.48x384 | 48, 384GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.4x32 | 4, 32GB, 8Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier | N/A|
| mx2.64x512 | 64, 512GB, 25Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
| mx2.8x64 | 8, 64GB, 16Gbps | Virtual | REDHAT_7_64, **REDHAT_8_64 (default)**| 100GB BLOCK | N/A | 300gb.5iops-tier, 300gb.10iops-tier, 600gb.5iops-tier, 600gb.10iops-tier, 900gb.5iops-tier, 900gb.10iops-tier, 1200gb.5iops-tier, 1200gb.10iops-tier, 1600gb.5iops-tier, 1600gb.10iops-tier, 2400gb.10iops-tier, 3000gb.10iops-tier, 4000gb.10iops-tier | N/A|
{: class="simple-tab-table"}
{: caption="Table. Memory flavors in Dallas." caption-side="bottom"}
{: #us-south-memory-table}
{: tab-title="Memory"}
{: tab-group="us-south-tables"}





