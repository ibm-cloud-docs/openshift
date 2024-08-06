---

copyright: 
  years: 2014, 2024
lastupdated: "2024-08-06"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, kubernetes, bare metal, flavors

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}

# Available flavors for bare metal
{: #flavors-bm}

Worker node flavors vary by cluster type, the zone where you want to create the cluster, the container platform, and the infrastructure provider that you want to use. To see the flavors available in your zone, run `ibmcloud oc flavors --zone <zone>`.

After you create GPU bare metal worker nodes in your {{site.data.keyword.redhat_openshift_notm}} cluster, [install the Node Feature Discovery and NVIDIA GPU operators for your cluster version](https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/getting-started.html){: external}.
{: note}


| Name and use case | Cores / Memory | Primary / Auxiliary disk | Network speed |
| --- | --- | --- | --- |
| **RAM-intensive bare metal, mb4c.20x64**: Maximize the RAM available to your worker nodes. This bare metal includes 2nd Generation Intel® Xeon® Scalable Processors with Intel® C620 Series chip sets for better performance for workloads such as machine learning, AI, and IoT. | 20 / 64 GB | 2 TB HDD / 960 GB SSD | 10000 Mbps |
| **RAM-intensive bare metal, mb4c.20x192**: Maximize the RAM available to your worker nodes. This bare metal includes 2nd Generation Intel® Xeon® Scalable Processors with Intel® C620 Series chip sets for better performance for workloads such as machine learning, AI, and IoT. | 20 / 192 GB | 2 TB HDD / 960 GB SSD | 10000 Mbps |
| **RAM-intensive bare metal, mb4c.20x384**: Maximize the RAM available to your worker nodes. This bare metal includes 2nd Generation Intel® Xeon® Scalable Processors with Intel® C620 Series chip sets for better performance for workloads such as machine learning, AI, and IoT. | 20 / 384 GB | 2 TB HDD / 960 GB SSD | 10000 Mbps |
| **GPU bare metal, mg4c.32x384.2xp100**: Choose this type for mathematically intensive workloads such as high-performance computing, machine learning, deep learning, or 3D applications. This flavor has two Tesla P100 physical cards that have two GPUs per card for a total of four GPUs. Note that this Pascal GPU flavor does not support the Data Center GPU Manager because of a known issue from NVIDIA. | 32 / 384 GB | 2 TB HDD / 960 GB SSD | 10000 Mbps |
| **Balanced bare metal, me4c.4x32**: Use for balanced workloads that require more compute resources than virtual machines offer. This bare metal includes 2nd Generation Intel® Xeon® Scalable Processors with Intel® C620 Series chip sets for better performance for workloads such as machine learning, AI, and IoT. | 4 / 32 GB | 2 TB HDD / 2 TB HDD | 10000 Mbps |
{: caption="Available bare metal flavors in {{site.data.keyword.openshiftlong_notm}}."}
