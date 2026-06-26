---

copyright:
  years: 2014, 2026
lastupdated: "2026-06-26"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, kubernetes, resource reserves

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}


# Worker node resource reserves
{: #resource-limit-node}

Understanding worker node resource reserves helps you plan cluster capacity and troubleshoot pod scheduling issues.
{: shortdesc}

{{site.data.keyword.openshiftlong_notm}} sets compute resource reserves that limit available compute resources on each worker node. Reserved memory, CPU resources, and process IDs (PIDs) can't be used by pods on the worker node, and reduces the allocatable resources on each worker node. When you initially deploy pods, if the worker node does not have enough allocatable resources, the deployment fails. Further, if pods exceed the worker node resource limit for memory and CPU, the pods are evicted. In Kubernetes, this limit is called a [hard eviction threshold](https://kubernetes.io/docs/concepts/scheduling-eviction/node-pressure-eviction/#hard-eviction-thresholds){: external}. For pods that exceed the PID limit, the pods receive as many PIDs as allocatable, but are not evicted based on PIDs.

## When to check resource reserves
{: #when-check-reserves}

Check worker node resource reserves when:
- Planning cluster capacity and determining how many worker nodes you need
- Troubleshooting pod scheduling failures or evictions
- Calculating available resources for your workloads
- Determining if you need to add more worker nodes to your cluster

If less PIDs, CPU, or memory is available than the worker node reserves, Kubernetes starts to evict pods to restore sufficient compute resources and PIDs. The pods reschedule onto another worker node if a worker node is available. If your pods are evicted frequently, add more worker nodes to your cluster or set [resource limits](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/#resource-requests-and-limits-of-pod-and-container){: external} on your pods.

## Understanding resource reserve tiers
{: #reserve-tiers}

The resources that are reserved on your worker node depend on the amount of PIDs, CPU, and memory that your worker node comes with. {{site.data.keyword.openshiftlong_notm}} defines PIDs, CPU, and memory tiers as shown in the following tables. If your worker node comes with compute resources in multiple tiers, a percentage of your PIDs, CPU, and memory resources is reserved for each tier.

Clusters also have process ID (PID) reservations and limits, to prevent a pod from using too many PIDs or ensure that enough PIDs exist for the `kubelet` and other {{site.data.keyword.openshiftlong_notm}} system components. If the PID reservations or limits are reached, Kubernetes does not create or assign new PIDs until enough processes are removed to free up existing PIDs. The total amount of PIDs on a worker node approximately corresponds to 8,000 PIDs per GB of memory on the worker node. For example, a worker node with 16 GB of memory has approximately 128,000 PIDs (`16 × 8,000 = 128,000`).

To review how much compute resources are currently used on your worker node, run [`oc top node`](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#top){: external}.
{: tip}

| Memory tier | % or amount reserved | `b3c.4x16` worker node (16 GB) example | `mg1c.28x256` worker node (256 GB) example|
|:-----------------|:-----------------|:-----------------|:-----------------|
| First 4 GB (0 - 4 GB) | 25% of memory | 1 GB | 1 GB|
| Next 4 GB (5 - 8 GB) | 20% of memory | 0.8 GB | 0.8 GB|
| Next 8 GB (9 - 16 GB) | 10% of memory | 0.8 GB | 0.8 GB|
| Next 112 GB (17 - 128 GB) | 6% of memory | N/A | 6.72 GB|
| Remaining GB (129 GB+) | 2% of memory | N/A | 2.54 GB|
| Additional reserve for [`kubelet` eviction](https://kubernetes.io/docs/concepts/scheduling-eviction/node-pressure-eviction/){: external} | 100 MB | 100 MB (flat amount) | 100 MB (flat amount)|
| **Total reserved** | **(varies)** | **2.7 GB of 16 GB total** | **11.96 GB of 256 GB total**|
{: class="simple-tab-table"}
{: caption="Worker node memory reserves by tier. The table shows memory tiers in the first column, the percentage or amount reserved in the second column, and example calculations for two different worker node sizes in the remaining columns." caption-side="bottom"}
{: summary="This table describes memory reserves for worker nodes. The first column lists memory tiers, the second column shows the percentage or amount reserved for each tier, and the remaining columns provide example calculations for a 16 GB worker node and a 256 GB worker node."}
{: #worker-memory-reserves}
{: tab-title="Worker node memory reserves by tier"}
{: tab-group="Worker Node"}

| CPU tier | % or amount reserved | `b3c.4x16` worker node (four cores) example | `mg1c.28x256` worker node (28 cores) example|
|:-----------------|:-----------------|:-----------------|:-----------------|
| First core (Core 1) | 6% cores | 0.06 cores | 0.06 cores|
| Next two cores (Cores 2 - 3) | 1% cores | 0.02 cores | 0.02 cores|
| Next two cores (Cores 4 - 5) | 0.5% cores | 0.005 cores | 0.01 cores|
| Remaining cores (Cores 6+) | 0.25% cores | N/A | 0.0575 cores|
| **Total reserved** | **(varies)** | **0.085 cores of four cores total** | **0.1475 cores of 28 cores total**|
{: class="simple-tab-table"}
{: caption="Worker node CPU reserves by tier. The table shows CPU tiers in the first column, the percentage or amount reserved in the second column, and example calculations for two different worker node sizes in the remaining columns." caption-side="bottom"}
{: summary="This table describes CPU reserves for worker nodes. The first column lists CPU tiers, the second column shows the percentage or amount reserved for each tier, and the remaining columns provide example calculations for a 4-core worker node and a 28-core worker node."}
{: #worker-cpu-reserves}
{: tab-title="Worker node CPU reserves by tier"}
{: tab-group="Worker Node"}

| Total PIDs | % reserved | % available to pod |
|:-----------------|:-----------------|:-----------------|
| < 200,000 | 20% PIDs | 35% PIDs |
| 200,000 - 499,999 | 10% PIDs  | 40% PIDs |
| ≥ 500,000 | 5% PIDs  | 45% PIDs  |
| `b3c.4x16` worker node: 126,878 PIDs | 25,376 PIDs (20%) | 44,407 PIDS (35%)  |
| `mg1c.28x256` worker node: 2,062,400 PIDs| 103,120 PIDs (5%) | 928,085 PIDs (45%) |
{: class="simple-tab-table"}
{: caption="Worker node PID reserves by tier. The table shows total PID ranges in the first column, the percentage reserved in the second column, the percentage available to pods in the third column, and example calculations for two different worker node sizes in the remaining rows." caption-side="bottom"}
{: summary="This table describes PID reserves for worker nodes. The first column lists total PID ranges, the second column shows the percentage reserved, the third column shows the percentage available to pods, and the remaining rows provide example calculations for a worker node with 126,878 PIDs and a worker node with 2,062,400 PIDs."}
{: #worker-pid-reserves}
{: tab-title="Worker node PID reserves by tier"}
{: tab-group="Worker Node"}

| Infrastructure provider | Disk | % of disk reserved |
|:------------------------|:-----|:-------------------|
| Classic | Secondary disk | 10% |
| VPC | Boot disk | 10% |
{: class="simple-tab-table"}
{: caption="Worker node disk ephemeral storage reserves. The table shows the infrastructure provider in the first column, the disk type in the second column, and the percentage of disk reserved in the third column." caption-side="bottom"}
{: summary="This table describes disk ephemeral storage reserves for worker nodes. The first column lists the infrastructure provider (Classic or VPC), the second column shows which disk is used, and the third column shows that 10% of disk space is reserved for both providers."}
{: #worker-memory-reserves-infra}
{: tab-title="Worker node disk reserves"}
{: tab-group="Worker Node"}

Sample worker node values are provided for example only. Your actual usage might vary slightly.
{: note}
