---

copyright: 
  years: 2014, 2023
lastupdated: "2023-10-04"

keywords: openshift, kubernetes, kubernetes environment, moving to kubernetes, moving to containers, clusters, cluster sizing

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}





# Sizing your cluster environment
{: #strategy}

With {{site.data.keyword.openshiftlong}}, you can quickly and securely deploy container workloads for your apps in production. Learn more so that when you plan your cluster strategy, you optimize your setup to make the most of [Kubernetes](https://kubernetes.io/){: external} automated deploying, scaling, and orchestration management capabilities.


Figuring out how many worker nodes you need in your cluster to support your workload is not an exact science. You might need to test different configurations and adapt. Good thing that you are using {{site.data.keyword.openshiftlong_notm}}, where you can add and remove worker nodes in response to your workload demands.


To get started on sizing your cluster, ask yourself the following questions.


## What else besides my app might use resources in the cluster?
{: #sizing_other}

Now let's add some other features that you might use.

* Keep in mind that the [worker nodes reserve certain amounts of CPU and memory resources](/docs/openshift?topic=openshift-planning_worker_nodes#resource_limit_node) to run required components, such as the operating system or container runtime.
* Consider whether your app pulls large or many images, which can take up local storage on the worker node.
* Decide whether you want to [integrate services](/docs/containers?topic=containers-supported_integrations#supported_integrations) into your cluster, such as [Helm](/docs/openshift?topic=openshift-helm) or [Prometheus](https://github.com/prometheus-operator/kube-prometheus){: external}. These integrated services and add-ons spin up pods that consume cluster resources.


## How many worker nodes do I need to handle my workload?
{: #sizing_workers}

Now that you have a good idea of what your workload looks like, let's map the estimated usage onto your available cluster configurations.

Estimate the max worker node capacity, which depends on what type of cluster you have. You don't want to max out worker node capacity in case a surge or other temporary event happens.

*  **Single zone clusters**: Plan to have at least three worker nodes in your cluster. Further, you want one extra node's worth of CPU and memory capacity available within the cluster. **Multizone clusters**: Plan to have at least two worker nodes per zone, so six nodes across three zones in total. Additionally, plan for the total capacity of your cluster to be at least 150% of your total workload's required capacity, so that if one zone goes down, you have resources available to maintain the workload.
* Align the app size and worker node capacity with one of the [available worker node flavors](/docs/openshift?topic=openshift-planning_worker_nodes#planning_worker_nodes). To see available flavors in a zone, run `ibmcloud oc flavors --zone <zone>`.
*   **Don't overload worker nodes**: To avoid your pods competing for CPU or running inefficiently, you must know what resources your apps require so that you can plan the number of worker nodes that you need. For example, if your apps require less resources than the resources that are available on the worker node, you can limit the number of pods that you deploy to one worker node. Keep your worker node at around 75% capacity to leave space for other pods that might need to be scheduled. If your apps require more resources than you have available on your worker node, use a different worker node flavor that can fulfill these requirements. You know that your worker nodes are overloaded when they frequently report back a status of `NotReady` or evict pods due to the lack of memory or other resources.
*   **Larger versus smaller worker node flavors**: Larger nodes can be more cost efficient than smaller nodes, particularly for workloads that are designed to gain efficiency when they process on a high-performance machine. However, if a large worker node goes down, you need to be sure that your cluster has enough capacity to safely reschedule all the workload pods onto other worker nodes in the cluster. Smaller worker can help you scale safely.
*   **Replicas of your app**: To determine the number of worker nodes that you want, you can also consider how many replicas of your app that you want to run. For example, if you know that your workload requires 32 CPU cores, and you plan to run 16 replicas of your app, each replica pod needs 2 CPU cores. If you want to run only one app pod per worker node, you can order an appropriate number of worker nodes for your cluster type to support this configuration.



## What type of cluster and flavors should I get?
{: #env_flavors}

**Types of clusters**: Decide whether you want a [single zone, multizone, or multiple cluster setup](/docs/openshift?topic=openshift-ha_clusters#ha_clusters). Multizone clusters are available in worldwide worldwide {{site.data.keyword.cloud_notm}} [multizone regions](/docs/openshift?topic=openshift-regions-and-zones#zones-mz). Also keep in mind that worker nodes vary by zone.

**Types of worker nodes**: In general, your intensive workloads are more suited to run on bare metal physical machines, whereas for cost-effective testing and development work, you might choose virtual machines on shared or dedicated hardware. [Check out the machine isolation and flavors that are available](/docs/openshift?topic=openshift-planning_worker_nodes#planning_worker_nodes). For a list of available flavors, see [VPC Gen 2 flavors](/docs/openshift?topic=openshift-vpc-flavors) or [Classic flavors](/docs/openshift?topic=openshift-classic-flavors).



## Do I use multiple clusters, or just add more workers to an existing cluster?
{: #env_multicluster}

The number of clusters that you create depends on your workload, company policies and regulations, and what you want to do with the computing resources. You can also review security information about this decision in [Container isolation and security](/docs/openshift?topic=openshift-security#container).

**Multiple clusters**: You need to set up [a global load balancer](/docs/openshift?topic=openshift-ha_clusters#multiple-clusters-glb) and copy and apply the same configuration YAML files in each to balance workloads across the clusters. Therefore, multiple clusters are generally more complex to manage, but can help you achieve important goals such as the following.
*  Comply with security policies that require you to isolate workloads.
*  Test how your app runs in a different version of {{site.data.keyword.redhat_openshift_notm}} or other cluster software such as Calico.
*  Create a cluster with your app in another region for higher performance for users in that geographical area.
*  Configure user access on the cluster-instance level instead of customizing and managing multiple RBAC policies to control access within a cluster at the namespace level.

**Fewer or single clusters**: Fewer clusters can help you to reduce operational effort and per-cluster costs for fixed resources. Instead of making more clusters, you can add worker pools for different flavors of computing resources available for the app and service components that you want to use. When you develop the app, the resources it uses are in the same zone, or otherwise closely connected in a multizone, so that you can make assumptions about latency, bandwidth, or correlated failures. However, it becomes even more important for you to organize your cluster by using namespaces, resource quotas, and labels.

## How can I set up my resources within the cluster?
{: #env_resources}

### Consider your worker node capacity
{: #env_resources_worker_capacity}

To get the most out of your worker node's performance, consider the following:
    - **Keep up your core strength**: Each machine has a certain number of cores. Depending on your app's workload, set a limit for the number of pods per core, such as 10.
    - **Avoid node overload**: Similarly, just because a node can contain more than 100 pods doesn't mean that you want it to. Depending on your app's workload, set a limit for the number of pods per node, such as 40.
    - Don't tap out your cluster bandwidth**: Keep in mind that network bandwidth on scaling virtual machines is around 1000 Mbps. If you need hundreds of worker nodes in a cluster, split it up into multiple clusters with fewer nodes, or order bare metal nodes.
    - **Sorting out your services**: Plan out how many services that you need for your workload before you deploy. Networking and port forwarding rules are put into Iptables. If you anticipate a larger number of services, such as more than 5,000 services, split up the cluster into multiple clusters.

### Provision different types of machines for a mix of computing resources
{: #env_resources_provision_types}

Everyone likes choices, right? With {{site.data.keyword.openshiftlong_notm}}, you have [a mix of flavors](/docs/openshift?topic=openshift-planning_worker_nodes#planning_worker_nodes) that you can deploy: from bare metal for intensive workloads to virtual machines for rapid scaling. Use labels or namespaces to organize deployments to your machines. When you create a deployment, limit it so that your app's pod deploys only on machines with the best mix of resources. For example, you might want to limit a database application to a bare metal machine with a significant amount of local disk storage like the `md1c.28x512.4x4tb`.

### Set up multiple namespaces when you have multiple teams and projects that share the cluster
{: #env_resources_multiple_namespaces}

Namespaces are kind of like a cluster within the cluster. They are a way to divide up cluster resources by using [resource quotas](https://kubernetes.io/docs/concepts/policy/resource-quotas/){: external} and [default limits](https://kubernetes.io/docs/tasks/administer-cluster/manage-resources/memory-default-namespace/){: external}. When you make new namespaces, be sure to set up proper [RBAC policies](/docs/openshift?topic=openshift-users#rbac) to control access. For more information, see [Share a cluster with namespaces](https://kubernetes.io/docs/tasks/administer-cluster/namespaces/){: external} in the Kubernetes documentation.

If you have a small cluster, a couple dozen users, and resources that are similar (such as different versions of the same software), you probably don't need multiple namespaces. You can use labels instead.

### Set resource quotas so that users in your cluster must use resource requests and limits
{: #env_resources_resource_quotas}

To ensure that every team has the necessary resources to deploy services and run apps in the cluster, you must set up [resource quotas](https://kubernetes.io/docs/concepts/policy/resource-quotas/){: external} for every namespace. Resource quotas determine the deployment constraints, such as the number of Kubernetes resources that you can deploy, and the amount of CPU and memory that can be consumed by those resources. After you set a quota, users must include resource requests and limits in their deployments.


