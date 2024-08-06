---

copyright: 
  years: 2014, 2024
lastupdated: "2024-08-06"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, kubernetes, bare metal, flavors

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}

# SDS flavors
{: #flavors-sds}

Worker node flavors vary by cluster type, the zone where you want to create the cluster, the container platform, and the infrastructure provider that you want to use. To see the flavors available in your zone, run `ibmcloud oc flavors --zone <zone>`.


| Name and use case | Cores / Memory | Primary / Secondary disk | Additional raw disks | Network speed |
| --- | --- | --- | --- | --- |
| **Data-intensive bare metal with SDS, me4c.4x32.1.9tb.ssd**: If you need extra local storage for performance, use this disk-heavy flavor that supports software-defined storage (SDS). This bare metal includes 2nd Generation Intel® Xeon® Scalable Processors with Intel® C620 Series chip sets for better performance for workloads such as machine learning, AI, and IoT. | 4 / 32 GB | 2 TB HDD / 960 GB SSD | 1.9 TB Raw SSD (device paths: `/dev/sdc`) | 10000 Mbps |
| **RAM-intensive bare metal with SDS, mb4c.20x64.2x1.9tb.ssd**: If you need extra local storage for performance, use this disk-heavy flavor that supports software-defined storage (SDS). Maximize the RAM available to your worker nodes. This bare metal includes 2nd Generation Intel® Xeon® Scalable Processors with Intel® C620 Series chip sets for better performance for workloads such as machine learning, AI, and IoT. | 20 / 64 GB | 2 TB HDD / 960 GB SSD | 2 disks, 1.9 TB Raw SSD (device paths: `/dev/sdc`, `/dev/sdd`) | 10000 Mbps |
| **RAM-intensive bare metal with SDS, mb4c.32x384.3.8tb.ssd**: If you need extra local storage for performance, use this disk-heavy flavor that supports software-defined storage (SDS). Maximize the RAM available to your worker nodes. This bare metal includes 2nd Generation Intel® Xeon® Scalable Processors with Intel® C620 Series chip sets for better performance for workloads such as machine learning, AI, and IoT. | 32 / 384 GB | 2 TB HDD / 960 GB SSD | 3.8 TB Raw SSD (device paths: `/dev/sdc`) | 10000 Mbps |
| **RAM-intensive bare metal with SDS, mb4c.32x384.6x3.8tb.ssd**: If you need extra local storage for performance, use this disk-heavy flavor that supports software-defined storage (SDS). Maximize the RAM available to your worker nodes. This bare metal includes 2nd Generation Intel® Xeon® Scalable Processors with Intel® C620 Series chip sets for better performance for workloads such as machine learning, AI, and IoT. | 32 / 384 GB | 2 TB HDD / 960 GB SSD | 6 disks, 3.8 TB Raw SSD (device paths: `/dev/sdc`, `/dev/sdd`, `/dev/sde`, `/dev/sdf`, `/dev/sdg`, `/dev/sdh`) | 10000 Mbps |
| **RAM-intensive bare metal with SDS, mb4c.32x768.3.8tb.ssd**: If you need extra local storage for performance, use this disk-heavy flavor that supports software-defined storage (SDS). Maximize the RAM available to your worker nodes. This bare metal includes 2nd Generation Intel® Xeon® Scalable Processors with Intel® C620 Series chip sets for better performance for workloads such as machine learning, AI, and IoT. | 32 / 768 GB | 2 TB HDD / 960 GB SSD | 3.8 TB Raw SSD (device paths: `/dev/sdc`) | 10000 Mbps |
{: caption="Available SDS flavors in {{site.data.keyword.openshiftlong_notm}}."}
