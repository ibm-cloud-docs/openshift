---

copyright: 
  years: 2014, 2022
lastupdated: "2022-03-22"

keywords: openshift

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Moving your environment to {{site.data.keyword.openshiftlong_notm}}
{: #strategy}

With {{site.data.keyword.openshiftlong}}, you can quickly and securely deploy container workloads for your apps in production. Learn more so that when you plan your cluster strategy, you optimize your setup to make the most of [Kubernetes](https://kubernetes.io/){: external} automated deploying, scaling, and orchestration management capabilities.
{: shortdesc}

## Moving your workloads to the {{site.data.keyword.cloud_notm}}
{: #cloud_workloads}

You have lots of reasons to move your workloads to {{site.data.keyword.cloud_notm}}: reducing total cost of ownership, increasing high availability for your apps in a secure and compliant environment, scaling up and down in respond to your user demand, and many more. {{site.data.keyword.openshiftlong_notm}} combines container technology with open source tools, such as Kubernetes so that you can build a cloud-native app that can migrate across different cloud environments, avoiding vendor lock-in.
{: shortdesc}

But how do you get to the cloud? What are your options along the way? And how do you manage your workloads after you get there?

Use this page to learn some strategies for your Kubernetes deployments on {{site.data.keyword.openshiftlong_notm}}. And always feel free to engage with our team on [Slack](https://ibm-cloud-success.slack.com){: external}.

Not on slack yet? [Request an invite!](https://cloud.ibm.com/kubernetes/slack){: external}
{: tip}

### What can I move to the {{site.data.keyword.cloud_notm}}?
{: #move_to_cloud}

With {{site.data.keyword.cloud_notm}}, you have flexibility to create {{site.data.keyword.redhat_openshift_notm}} clusters in [off-premises, on-premises, or hybrid cloud environments](/docs/containers?topic=containers-cs_ov#differentiation). The following table provides some examples of what types of workloads that users typically move to the various types of clouds. You might also choose a hybrid approach where you have clusters that run in both environments.
{: shortdesc}

| Workload | {{site.data.keyword.containershort_notm}} off-prem | on-prem |
| --- | --- | --- |
| DevOps enablement tools | Yes | |
| Developing and testing apps | Yes | |
| Apps have major shifts in demand and need to scale rapidly | Yes | |
| Business apps such as CRM, HCM, ERP, and E-commerce | Yes | |
| Collaboration and social tools such as email | Yes | |
| RHEL workloads | Yes | |
| Bare metal and GPU compute resources | Yes | Yes |
| PCI and HIPAA-compliant workloads | Yes | Yes |
| Legacy apps with platform and infrastructure constraints and dependencies | | Yes |
| Proprietary apps with strict designs, licensing, or heavy regulations | | Yes |
{: caption="{{site.data.keyword.cloud_notm}} implementations support your workloads" caption-side="top"}

**Ready to run workloads off-premises in {{site.data.keyword.openshiftlong_notm}}?**

Great! You're already in our public cloud documentation. Keep reading for more strategy ideas, or hit the ground running by [creating a cluster now](/docs/containers?topic=containers-getting-started).

**Want to run workloads in both on-premises and off-premises clouds?**

Explore [{{site.data.keyword.satellitelong_notm}}](/docs/satellite?topic=satellite-about) to extend the flexibility and scalability of {{site.data.keyword.cloud_notm}} into your on-premises, edge, or other cloud provider environments.

### Can I automate my infrastructure deployments?
{: #infra_packaging}

If you want to run your app in multiple clusters, public and private environments, or even multiple cloud providers, you might wonder how you can make your deployment strategy work across these environments.

You can use the open source [Terraform](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-getting-started#getting-started) tool to automate the provisioning of {{site.data.keyword.cloud_notm}} infrastructure, including Kubernetes clusters. Follow along with this tutorial to [plan, create, and update deployment environments](/docs/solution-tutorials?topic=solution-tutorials-plan-create-update-deployments#plan-create-update-deployments). After you create a cluster, you can also set up the [{{site.data.keyword.openshiftlong_notm}} cluster autoscaler](/docs/containers?topic=containers-cluster-scaling-classic-vpc) so that your worker pool scales up and down worker nodes in response to your workload's resource requests.</dd>

### What kind of apps can I run? Can I move existing apps, or do I need to develop new apps?
{: #app_kinds}

Your containerized app must be able to run on the supported operating system, RHEL 7. You also want to consider the statefulness of your app. For more information about the kinds of apps that can run in {{site.data.keyword.openshiftlong_notm}}, see [Planning app deployments](/docs/openshift?topic=openshift-plan_deploy#app_types).

If you already have an app, you can [migrate it to {{site.data.keyword.openshiftlong_notm}}](/docs/openshift?topic=openshift-plan_deploy#migrate_containerize). If you want to develop a new app, check out the [guidelines for developing stateless, cloud-native apps](/docs/openshift?topic=openshift-plan_deploy#12factor).

### What about serverless apps?
{: #apps_serverless}

You can run serverless apps and jobs through the [{{site.data.keyword.codeenginefull_notm}}](/docs/codeengine?topic=codeengine-getting-started) service. {{site.data.keyword.codeengineshort}} can also build your images for you. 
{: shortdesc}

### What knowledge and technical skills are good to have before I move my apps to {{site.data.keyword.openshiftlong_notm}}?
{: #knowledge}

{{site.data.keyword.redhat_openshift_notm}} is designed to provide capabilities to two main personas, the cluster admin and the app developer. Each persona uses different technical skills to successfully run and deploy apps to a cluster.
{: shortdesc}

**What are a cluster admin's main tasks and technical knowledge?**

As a cluster admin, you are responsible to set up, operate, secure, and manage the {{site.data.keyword.cloud_notm}} infrastructure of your cluster. Typical tasks include:
- Size the cluster to provide enough capacity for your workloads.
- Design a cluster to meet the high availability, disaster recovery, and compliance standards of your company.
- Secure the cluster by setting up user permissions and limiting actions within the cluster to protect your compute resources, your network, and data.
- Plan and manage network communication between infrastructure components to ensure network security, segmentation, and compliance.
- Plan persistent storage options to meet data residency and data protection requirements.

The cluster admin persona must have a broad knowledge that includes compute, network, storage, security, and compliance. In a typical company, this knowledge is spread across multiple specialists, such as System Engineers, System Administrators, Network Engineers, Network Architects, IT Managers, or Security and Compliance Specialists. Consider assigning the cluster admin role to multiple people in your company so that you have the required knowledge to successfully operate your cluster.

**What are an app developer's main tasks and technical skills?**

As a developer, you design, create, secure, deploy, test, run, and monitor cloud-native, containerized apps in an {{site.data.keyword.redhat_openshift_notm}} cluster. To create and run these apps, you must be familiar with the concept of microservices, the [12-factor app](/docs/openshift?topic=openshift-plan_deploy#12factor) guidelines, [Docker and containerization principles](https://www.docker.com/), and available [{{site.data.keyword.redhat_openshift_notm}} deployment options](/docs/containers?topic=containers-plan_deploy).

{{site.data.keyword.redhat_openshift_notm}} and {{site.data.keyword.openshiftlong_notm}} provide multiple options for how to [expose an app and keep an app private](/docs/containers?topic=containers-cs_network_planning), [add persistent storage](/docs/containers?topic=containers-storage_planning), [integrate other services](/docs/containers?topic=containers-ibm-3rd-party-integrations), and how you can [secure your workloads and protect sensitive data](/docs/openshift?topic=openshift-security#container). Before you move your app to a cluster in {{site.data.keyword.openshiftlong_notm}}, verify that you can run your app as a containerized app on the supported RHEL 7 operating system and that {{site.data.keyword.redhat_openshift_notm}} and {{site.data.keyword.openshiftlong_notm}} provide the capabilities that your workload needs.

**Do cluster administrators and developers interact with each other?**

Yes. Cluster administrators and developers must interact frequently so that cluster administrators understand workload requirements to provide this capability in the cluster, and so that developers know about available limitations, integrations, and security principles that they must consider in their app development process.

## Sizing your {{site.data.keyword.redhat_openshift_notm}} cluster to support your workload
{: #sizing}

Figuring out how many worker nodes you need in your cluster to support your workload is not an exact science. You might need to test different configurations and adapt. Good thing that you are using {{site.data.keyword.openshiftlong_notm}}, where you can add and remove worker nodes in response to your workload demands.
{: shortdesc}

To get started on sizing your cluster, ask yourself the following questions.

### How many resources does my app require?
{: #sizing_resources}

First, let's begin with your existing or project workload usage.

1. Calculate your workload's average CPU and memory usage. For example, you might view the Task Manager on a Windows machine, or run the `top` command on a Mac or Linux. You might also use a metrics service and run reports to calculate workload usage.
2. Anticipate the number of requests that your workload must serve so that you can decide how many app replicas you want to handle the workload. For example, you might design an app instance to handle 1000 requests per minute and anticipate that your workload must serve 10000 requests per minute. If so, you might decide to make 12 app replicas, with 10 to handle the anticipated amount and an extra 2 for surge capacity.

### What else besides my app might use resources in the cluster?
{: #sizing_other}

Now let's add some other features that you might use.

1. Keep in mind that the [worker nodes reserve certain amounts of CPU and memory resources](/docs/openshift?topic=openshift-planning_worker_nodes#resource_limit_node) to run required components, such as the operating system or container runtime.
2. Consider whether your app pulls large or many images, which can take up local storage on the worker node.
3. Decide whether you want to [integrate services](/docs/containers?topic=containers-supported_integrations#supported_integrations) into your cluster, such as [Helm](/docs/containers?topic=containers-helm) or [Prometheus](https://github.com/prometheus-operator/kube-prometheus){: external}. These integrated services and add-ons spin up pods that consume cluster resources.

### What type of availability do I want my workload to have?
{: #sizing_availability}

Don't forget that you want your workload to be up as much as possible! As such, you might need replicas of your workload pods.

1. Plan out your strategy for [highly available clusters](/docs/openshift?topic=openshift-ha_clusters#ha_clusters), such as deciding between single or multizone clusters.
2. Review [highly available deployments](/docs/openshift?topic=openshift-plan_deploy#highly_available_apps) to help decide how you can make your app available.

### How many worker nodes do I need to handle my workload?
{: #sizing_workers}

Now that you have a good idea of what your workload looks like, let's map the estimated usage onto your available cluster configurations.

1. Estimate the max worker node capacity, which depends on what type of cluster you have. You don't want to max out worker node capacity in case a surge or other temporary event happens.
    *  **Single zone clusters**: Plan to have at least three worker nodes in your cluster. Further, you want one extra node's worth of CPU and memory capacity available within the cluster.
    *  **Multizone clusters**: Plan to have at least two worker nodes per zone, so six nodes across three zones in total. Additionally, plan for the total capacity of your cluster to be at least 150% of your total workload's required capacity, so that if one zone goes down, you have resources available to maintain the workload.
2. Align the app size and worker node capacity with one of the [available worker node flavors](/docs/openshift?topic=openshift-planning_worker_nodes#planning_worker_nodes). To see available flavors in a zone, run `ibmcloud oc flavors --zone <zone>`.
    *   **Don't overload worker nodes**: To avoid your pods competing for CPU or running inefficiently, you must know what resources your apps require so that you can plan the number of worker nodes that you need. For example, if your apps require less resources than the resources that are available on the worker node, you can limit the number of pods that you deploy to one worker node. Keep your worker node at around 75% capacity to leave space for other pods that might need to be scheduled. If your apps require more resources than you have available on your worker node, use a different worker node flavor that can fulfill these requirements. You know that your worker nodes are overloaded when they frequently report back a status of `NotReady` or evict pods due to the lack of memory or other resources.
    *   **Larger vs. smaller worker node flavors**: Larger nodes can be more cost efficient than smaller nodes, particularly for workloads that are designed to gain efficiency when they process on a high-performance machine. However, if a large worker node goes down, you need to be sure that your cluster has enough capacity to gracefully reschedule all the workload pods onto other worker nodes in the cluster. Smaller worker can help you scale more gracefully.
    *   **Replicas of your app**: To determine the number of worker nodes that you want, you can also consider how many replicas of your app that you want to run. For example, if you know that your workload requires 32 CPU cores, and you plan to run 16 replicas of your app, each replica pod needs 2 CPU cores. If you want to run only one app pod per worker node, you can order an appropriate number of worker nodes for your cluster type to support this configuration.

### How do I monitor resource usage and capacity in my cluster?
{: #sizing_manage}

Now that you have a good estimate of your app size and the worker nodes that you need to run your workload, you can deploy your app and continuously monitor performance to maximize your compute resource usage.

1. [Create your cluster](/docs/containers?topic=containers-clusters) with the worker pool flavor and number of worker nodes that you [previously estimated](#sizing_workers).
2. Review what compute resources your cluster uses by default and calculate the remaining cluster capacity that you can use for your workloads.
    1. With the {{site.data.keyword.cloud_notm}} IAM **Manager** service access role for the cluster in all namespaces: [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).
    2. Find the CPU and memory usage across all worker nodes. From the [{{site.data.keyword.redhat_openshift_notm}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, you can also click your cluster and review the **Cluster Insights** card.
        ```sh
        oc top nodes
        ```
        {: pre}

        Example output
        ```sh
        NAME            CPU(cores)   CPU%   MEMORY(bytes)   MEMORY%   
        10.xxx.xx.xxx   149m         7%     2402Mi          84%       
        10.xxx.xx.xxx   122m         6%     2395Mi          83%       
        10.xxx.xx.xxx   144m         7%     2376Mi          83%   
        ```
        {: screen}

    3. Add the CPU and memory usage amounts to the [worker node resource reserves](/docs/openshift?topic=openshift-planning_worker_nodes#resource_limit_node) that are set for each worker node by default.
    4. Subtract the worker node reserved and default app usage amounts from the total worker node size. This amount represents the total compute resources of your worker nodes before you deploy any apps or other workloads.
3. [Deploy your apps](/docs/containers?topic=containers-deploy_app) to the cluster, and make sure to [set resource requests and limits](/docs/containers?topic=containers-app#resourcereq) based on the [app size that you previously estimated](#sizing_resources) for your apps, to limit the amount of compute resources the apps can consume.
4. Deploy any add-ons, plug-ins, or other cloud services that you want to use.
5. Review what compute resources your workloads consume and calculate the remaining cluster capacity to deploy additional apps or scale existing apps.
    1. With at least the {{site.data.keyword.cloud_notm}} IAM **Reader** service access role for the cluster in all namespaces: [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).
    2. List the pods that run in your cluster.
        ```sh
        oc get pods --all-namespaces
        ```
        {: pre}

    3. Get the details of a pod. Note the **limits** and **request** map of the CPU and memory.
        ```sh
        oc get pod -n <project> <pod> -o=jsonpath='{range .spec.containers[*]}  {.name}:{.resources}{"\n"}{end}'
        ```
        {: pre}

    4. Repeat the previous step for each pod in your cluster.
    5. Add up the resource requests and limits of the apps that you deployed by default.
6. Subtract the sum of your workload resource limits that you estimated in Step 5 from the available compute resources of your worker nodes that you estimated in Step 2. The remaining amount is the extra compute resources that you have to run new workloads or to scale your existing workloads.
7. For workloads that need to scale up and down in response to resource requests, set up the [horizontal pod autoscaler](/docs/openshift?topic=openshift-update_app#app_scaling) and [cluster worker pool autoscaler](/docs/containers?topic=containers-cluster-scaling-classic-vpc).
8. [Set up monitoring tools](/docs/containers?topic=containers-health-monitor#view_metrics) to continue reviewing CPU and memory usage across worker nodes in your cluster.
9. Run performance tests to continue refining the number of worker nodes you need in your cluster, with representative latency, scalability, data set, and workload requirements.



## Structuring your {{site.data.keyword.redhat_openshift_notm}} environment
{: #kube_env}

Your {{site.data.keyword.openshiftlong_notm}} is linked to one IBM Cloud infrastructure portfolio only. Within your account, you can create clusters that are composed of a master and various worker nodes. IBM manages the master, and you can create a mix of worker pools that pool together individual machines of the same flavor, or memory and CPU specs. Within the cluster, you can further organize resources by using namespaces and labels. Choose the right mix of cluster, flavors, and organization strategies so that you can make sure that your teams and workloads get the resources that they need.
{: shortdesc}

### What type of cluster and flavors should I get?
{: #env_flavors}

**Types of clusters**: Decide whether you want a [single zone, multizone, or multiple cluster setup](/docs/openshift?topic=openshift-ha_clusters#ha_clusters). Multizone clusters are available in worldwide worldwide {{site.data.keyword.cloud_notm}} [multizone regions](/docs/openshift?topic=openshift-regions-and-zones#zones-mz). Also keep in mind that worker nodes vary by zone.

**Types of worker nodes**: In general, your intensive workloads are more suited to run on bare metal physical machines, whereas for cost-effective testing and development work, you might choose virtual machines on shared or dedicated hardware. [Check out the machine isolation and flavors that are available](/docs/openshift?topic=openshift-planning_worker_nodes#planning_worker_nodes). For a list of available flavors, see [VPC Gen 2 flavors](/docs/containers?topic=containers-vpc-gen2-flavors) or [Classic flavors](/docs/containers?topic=containers-classic-flavors).



### Do I use multiple clusters, or just add more workers to an existing cluster?
{: #env_multicluster}

The number of clusters that you create depends on your workload, company policies and regulations, and what you want to do with the computing resources. You can also review security information about this decision in [Container isolation and security](/docs/openshift?topic=openshift-security#container).

**Multiple clusters**: You need to set up [a global load balancer](/docs/openshift?topic=openshift-ha_clusters#multiple_clusters) and copy and apply the same configuration YAML files in each to balance workloads across the clusters. Therefore, multiple clusters are generally more complex to manage, but can help you achieve important goals such as the following.
*  Comply with security policies that require you to isolate workloads.
*  Test how your app runs in a different version of {{site.data.keyword.redhat_openshift_notm}} or other cluster software such as Calico.
*  Create a cluster with your app in another region for higher performance for users in that geographical area.
*  Configure user access on the cluster-instance level instead of customizing and managing multiple RBAC policies to control access within a cluster at the namespace level.

**Fewer or single clusters**: Fewer clusters can help you to reduce operational effort and per-cluster costs for fixed resources. Instead of making more clusters, you can add worker pools for different flavors of computing resources available for the app and service components that you want to use. When you develop the app, the resources it uses are in the same zone, or otherwise closely connected in a multizone, so that you can make assumptions about latency, bandwidth, or correlated failures. However, it becomes even more important for you to organize your cluster by using namespaces, resource quotas, and labels.

### How can I set up my resources within the cluster?
{: #env_resources}

#### Consider your worker node capacity
{: #env_resources_worker_capacity}

To get the most out of your worker node's performance, consider the following:
    - **Keep up your core strength**: Each machine has a certain number of cores. Depending on your app's workload, set a limit for the number of pods per core, such as 10.
    - **Avoid node overload**: Similarly, just because a node can contain more than 100 pods doesn't mean that you want it to. Depending on your app's workload, set a limit for the number of pods per node, such as 40.
    - Don't tap out your cluster bandwidth**: Keep in mind that network bandwidth on scaling virtual machines is around 1000 Mbps. If you need hundreds of worker nodes in a cluster, split it up into multiple clusters with fewer nodes, or order bare metal nodes.
    - **Sorting out your services**: Plan out how many services that you need for your workload before you deploy. Networking and port forwarding rules are put into Iptables. If you anticipate a larger number of services, such as more than 5,000 services, split up the cluster into multiple clusters.

#### Provision different types of machines for a mix of computing resources
{: #env_resources_provision_types}

Everyone likes choices, right? With {{site.data.keyword.openshiftlong_notm}}, you have [a mix of flavors](/docs/openshift?topic=openshift-planning_worker_nodes#planning_worker_nodes) that you can deploy: from bare metal for intensive workloads to virtual machines for rapid scaling. Use labels or namespaces to organize deployments to your machines. When you create a deployment, limit it so that your app's pod deploys only on machines with the right mix of resources. For example, you might want to limit a database application to a bare metal machine with a significant amount of local disk storage like the `md1c.28x512.4x4tb`.

#### Set up multiple namespaces when you have multiple teams and projects that share the cluster
{: #env_resources_multiple_namespaces}

Namespaces are kind of like a cluster within the cluster. They are a way to divide up cluster resources by using [resource quotas](https://kubernetes.io/docs/concepts/policy/resource-quotas/){: external} and [default limits](https://kubernetes.io/docs/tasks/administer-cluster/manage-resources/memory-default-namespace/){: external}. When you make new namespaces, be sure to set up proper [RBAC policies](/docs/openshift?topic=openshift-users#rbac) to control access. For more information, see [Share a cluster with namespaces](https://kubernetes.io/docs/tasks/administer-cluster/namespaces/){: external} in the Kubernetes documentation.

If you have a small cluster, a couple dozen users, and resources that are similar (such as different versions of the same software), you probably don't need multiple namespaces. You can use labels instead.

#### Set resource quotas so that users in your cluster must use resource requests and limits
{: #env_resources_resource_quotas}

To ensure that every team has the necessary resources to deploy services and run apps in the cluster, you must set up [resource quotas](https://kubernetes.io/docs/concepts/policy/resource-quotas/) for every namespace. Resource quotas determine the deployment constraints for a project, such as the number of Kubernetes resources that you can deploy, and the amount of CPU and memory that can be consumed by those resources. After you set a quota, users must include resource requests and limits in their deployments.

#### Organize your Kubernetes objects with labels
{: #env_resources_kube_labels}

To organize and select your Kubernetes resources such as `pods` or `nodes`, [use Kubernetes labels](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/){: external}. By default, {{site.data.keyword.openshiftlong_notm}} applies some labels, including `arch`, `os`, `region`, `zone`, and `machine-type`.

Example use cases for labels include [limiting network traffic to edge worker nodes](/docs/containers?topic=containers-edge), [deploying an app to a GPU machine](/docs/containers?topic=containers-deploy_app#gpu_app), and [restricting your app workloads](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/){: external} to run on worker nodes that meet certain flavor or SDS capabilities, such as bare metal worker nodes. To see what labels are already applied to a resource, use the `oc get` command with the `--show-labels` flag.

To apply labels to worker nodes, [create your worker pool](/docs/openshift?topic=openshift-add_workers#add_pool) with labels or [update an existing worker pool](/docs/openshift?topic=openshift-add_workers#worker_pool_labels).


### How can I keep my cluster in a supported state?
{: #updating_kube}

Make sure that your cluster always runs a [supported {{site.data.keyword.redhat_openshift_notm}} version](/docs/openshift?topic=openshift-openshift_changelog). When a new {{site.data.keyword.redhat_openshift_notm}} minor version is released, an older version is shortly deprecated after and then becomes unsupported. For more information, see [Updating the master](/docs/containers?topic=containers-update#master) and [worker nodes](/docs/containers?topic=containers-update#worker_node).





## Making your resources highly available
{: #kube_ha}

While no system is entirely failsafe, you can take steps to increase the high availability of your apps and services in {{site.data.keyword.openshiftlong_notm}}.
{: shortdesc}

Review more information about making resources highly available.
* [Reduce potential points of failure](/docs/openshift?topic=openshift-ha#ha).
* [Create multizone clusters](/docs/openshift?topic=openshift-ha_clusters#ha_clusters).
* [Plan highly available deployments](/docs/openshift?topic=openshift-plan_deploy#highly_available_apps) that use features such as replica sets and pod anti-affinity across multizones.
* [Run containers that are based on images in a cloud-based public registry](/docs/containers?topic=containers-images).
* [Plan data storage](/docs/openshift?topic=openshift-storage_planning#persistent_storage_overview). Especially for multizone clusters, consider using a cloud service such as [{{site.data.keyword.cloudant_short_notm}}](/docs/Cloudant?topic=Cloudant-getting-started-with-cloudant) or [{{site.data.keyword.cos_full_notm}}](/docs/cloud-object-storage?topic=cloud-object-storage-getting-started-cloud-object-storage).
* For multizone clusters, enable a [load balancer service](/docs/openshift?topic=openshift-loadbalancer#multi_zone_config) or the Ingress [multizone load balancer](/docs/containers?topic=containers-ingress-types) to expose your apps publicly.




