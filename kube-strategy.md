---

copyright: 
  years: 2014, 2024
lastupdated: "2024-03-15"


keywords: openshift, kubernetes, kubernetes environment, moving to kubernetes, moving to containers, clusters, cluster sizing

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Creating a cluster environment strategy
{: #strategy}

Figuring out what your cluster setup must be to support your workload is not an exact science. You might need to test different configurations and adapt. To get started planning and sizing your cluster, ask yourself the following questions.
{: shortdesc}


## What type of cluster should I get?
{: #env_flavors}

- **Classic or VPC**? Openshift? If you choose a classic cluster, consider [creating a reservation](/docs/openshift?topic=openshift-reservations) to lock in a discount over 1 or 3 year terms for your worker nodes. After you create the cluster, add worker pools that use the reserved instances. Typical savings range between 30-50% compared to regular worker node costs.
- **Number of clusters**: How many clusters you use could impact the type of cluster you need. If you only need one cluster, then a single zone or even multizone cluster might work. Learn more about the differences between a [single zone, multizone, or multiple cluster setup](/docs/openshift?topic=openshift-ha_clusters#ha_clusters).
- **Figure out where you want it**: Decide which locations you want to have a cluster in. Where you want it might also inform how many clusters or the type of clusters you need. If you need multiple locations, check out a [multizone](/docs/openshift?topic=openshift-regions-and-zones#zones-mz) or multiple cluster setup.
- **Consider work node flavors**: [Worker node flavors](#env_flavors_node) can vary by zone, so when you are choosing a cluster type, think about which worker node flavors might work best for your setup.

## Do I actually need multiple clusters or can I just add more workers to one cluster?
{: #env_multicluster}

The number of clusters that you create depends on your workload, company policies and regulations, and what you want to do with the computing resources. You can also review security information about this decision in [Container isolation and security](/docs/openshift?topic=openshift-security#container).

- **Multiple clusters**: Multiple clusters are generally more complex to manage, but can help you achieve important goals such as the following.
    *  Comply with security policies that require you to isolate workloads.
    *  Test how your app runs in a different version of {{site.data.keyword.redhat_openshift_notm}} or other cluster software such as Calico.
    *  Create a cluster with your app in another region for higher performance for users in that geographical area.
    *  Configure user access on the cluster-instance level instead of customizing and managing multiple RBAC policies to control access within a cluster at the namespace level.
    * Keep in mind that network bandwidth on scaling virtual machines is around 1000 Mbps. If you need hundreds of worker nodes in a cluster, split it up into multiple clusters with fewer nodes, or order bare metal nodes.

- **More worker nodes**: Fewer clusters can help you to reduce operational effort and per-cluster costs for fixed resources. Instead of making more clusters, you can add worker pools for different flavors of computing resources available for your app and service components. When you develop the app, the resources it uses are in the same zone, or otherwise closely connected in a multizone, so that you can make assumptions about latency, bandwidth, or correlated failures. However, it becomes even more important for you to organize your cluster by using namespaces, resource quotas, and labels.
{: #env_resources}

## How do I name my clusters?
{: #naming}

Consider giving clusters unique names across resource groups and regions in your account to avoid naming conflicts. You can't rename a cluster after it is created.


## How many worker nodes do I need to handle my workload?
{: #sizing_workers}

*  **Single zone clusters**: Plan to have at least three worker nodes in your cluster. Further, you want one extra node's worth of CPU and memory capacity available within the cluster. 

* **Multizone clusters**: Plan to have at least two worker nodes per zone, so six nodes across three zones in total. Additionally, plan for the total capacity of your cluster to be at least 150% of your total workload's required capacity, so that if one zone goes down, you have resources available to maintain the workload.

* **Required resources**: If your apps require less resources than the resources that are available on the worker node, you might be able to limit the number of pods that you deploy to one worker node. 




## What type of worker node flavors should I get?
{: #env_flavors_node}

It depends. As you decide, consider the following.

- **Machine type**: Everyone likes choices, right? With {{site.data.keyword.openshiftlong_notm}}, you have [a mix of machine types](/docs/openshift?topic=openshift-planning_worker_nodes#planning_worker_nodes) that you can deploy: from bare metal for intensive workloads to virtual machines for rapid scaling. You can set limits to ensure that certain types of apps are deployed on certain machine types. For a list of available flavors, see [VPC Gen 2 flavors](/docs/openshift?topic=openshift-vpc-flavors) or [Classic flavors](/docs/openshift?topic=openshift-classic-flavors).

- **Size**: Larger nodes can be more cost efficient than smaller nodes, particularly for workloads that are designed to gain efficiency when they process on a high-performance machine. However, if a large worker node goes down, you need to be sure that your cluster has enough capacity to safely reschedule all the workload pods onto other worker nodes in the cluster. Smaller worker can help you scale safely. [Learn more about capacity](#env_resources_worker_capacity).

 - **Cost**: In general, your intensive workloads are more suited to run on bare metal physical machines, whereas for cost-effective testing and development work, you might choose virtual machines on shared or dedicated hardware. [Check out the machine isolation and flavors that are available](/docs/openshift?topic=openshift-planning_worker_nodes#planning_worker_nodes).
-  **Location**: Keep in mind that worker node flavors vary by zone.





## How do I determine worker node capacity for my resources?
{: #env_resources_worker_capacity}

To get the most out of your worker node's performance, consider the following as you set up your resources:

- **Consider what your app is doing**: Start by aligning the app size with the capacity of one of the [available worker node flavors](/docs/openshift?topic=openshift-planning_worker_nodes#planning_worker_nodes). Also consider thing like whether your app pulls large or many images, since they can take up local storage on the worker node.

- **Keep up your core strength**: Each machine has a certain number of cores. Depending on your app's workload, set a limit for the number of pods per core, such as 10. 

- **Avoid node overload**: Keep your worker node at around 75% capacity to leave space for other pods that might need to be scheduled. If your apps require more resources than you have available on your worker node, use a different worker node flavor that can fulfill these requirements. Depending on your app's workload, set a limit for the number of pods per node, such as 40.

- **Choose services**: Plan out how many services that you need for your workload before you deploy. Networking and port forwarding rules are put into Iptables. You can also [integrate services](/docs/containers?topic=containers-supported_integrations#supported_integrations), such as [Helm](/docs/openshift?topic=openshift-helm) or [Prometheus](https://github.com/prometheus-operator/kube-prometheus){: external}. These integrated services and add-ons spin up pods that consume cluster resources. If you anticipate a larger number of services, such as more than 5,000 services, split up the cluster into multiple clusters.

- **Replicas of your app**: To determine the number of worker nodes that you want, you can also consider how many replicas of your app that you want to run. For example, if you know that your workload requires 32 CPU cores, and you plan to run 16 replicas of your app, each replica pod needs 2 CPU cores. If you want to run only one app pod per worker node, you can order an appropriate number of worker nodes for your cluster type to support this configuration.

- **Leave room for runtime requirements**: [Worker nodes must reserve certain amounts of CPU and memory resources](/docs/openshift?topic=openshift-planning_worker_nodes#resource_limit_node) to run required components, such as the operating system or container runtime.



## How do I manage teams and projects?
{: #env_resources_multiple_namespaces}

Set up multiple namespaces when you have multiple teams and projects that share the cluster. Namespaces are kind of like a cluster within the cluster. They are a way to divide up cluster resources by using [resource quotas](https://kubernetes.io/docs/concepts/policy/resource-quotas/){: external} and [default limits](https://kubernetes.io/docs/tasks/administer-cluster/manage-resources/memory-default-namespace/){: external}. When you make new namespaces, be sure to set up proper [RBAC policies](/docs/openshift?topic=openshift-users#rbac) to control access. For more information, see [Share a cluster with namespaces](https://kubernetes.io/docs/tasks/administer-cluster/namespaces/){: external} in the Kubernetes documentation.

If you have a small cluster, a couple dozen users, and resources that are similar (such as different versions of the same software), you probably don't need multiple namespaces. You can use labels instead.

##  How do I manage resource requests and limits?
{: #env_resources_resource_quotas}

To ensure that every team has the necessary resources to deploy services and run apps in the cluster, you must set up [resource quotas](https://kubernetes.io/docs/concepts/policy/resource-quotas/){: external} for every namespace. Resource quotas determine the deployment constraints, such as the number of Kubernetes resources that you can deploy, and the amount of CPU and memory that can be consumed by those resources. After you set a quota, users must include resource requests and limits in their deployments.

When you create a deployment, also limit it so that your app's pod deploys only on machines with the best mix of resources. For example, you might want to limit a database application to a bare metal machine with a significant amount of local disk storage like the `md1c.28x512.4x4tb`.

