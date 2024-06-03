---

copyright: 
  years: 2014, 2024
lastupdated: "2024-06-03"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, kubernetes, infrastructure, rbac, policy, providers, benefits

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Understanding {{site.data.keyword.openshiftlong_notm}}
{: #overview}

Learn more about [{{site.data.keyword.openshiftlong}}](https://www.ibm.com/products/openshift){: external}, its capabilities, and the options that are available to you to customize the cluster to your needs.
{: shortdesc}

{{site.data.keyword.openshiftlong_notm}} is a managed offering to create your own {{site.data.keyword.redhat_openshift_notm}} cluster of compute hosts to deploy and manage containerized apps on {{site.data.keyword.cloud_notm}}. {{site.data.keyword.openshiftlong_notm}} provides intelligent scheduling, self-healing, horizontal scaling, service discovery and load balancing, automated rollouts and rollbacks, and secret and configuration management for your apps. Combined with an intuitive user experience, built-in security and isolation, and advanced tools to secure, manage, and monitor your cluster workloads, you can rapidly deliver highly available and secure containerized apps in the public cloud.


Review frequently asked questions and key technologies that {{site.data.keyword.openshiftlong_notm}} uses.


## What is Kubernetes?
{: #what-is-kube-overview}

Kubernetes is an open source platform for managing containerized workloads and services across multiple hosts, and offers management tools for deploying, automating, monitoring, and scaling containerized apps with minimal to no manual intervention.

![Kubernetes certification badge](images/certified-kubernetes-color.svg "Deployment setup"){: caption="Figure 1. This badge indicates Kubernetes certification for IBM Cloud Container Service." caption-side="bottom"}

The open source project, Kubernetes, combines running a containerized infrastructure with production workloads, open source contributions, and Docker container management tools. The Kubernetes infrastructure provides an isolated and secure app platform for managing containers that is portable, extensible, and self-healing in case of a failover. For more information, see [What is Kubernetes?](https://www.ibm.com/topics/kubernetes){: external}.

Learn more about the key concepts of Kubernetes as illustrated in the following image.


![Example deployment and namespaces](images/k8-namespace.svg "Deployment setup"){: caption="Figure 2. A description of key concepts for Kubernetes" caption-side="bottom"}


Account
:   Your account refers to your {{site.data.keyword.cloud_notm}} account.

Cluster, worker pool, and worker node
:   A Kubernetes cluster consists of a master and one or more compute hosts that are called worker nodes. Worker nodes are organized into worker pools of the same flavor, or profile of CPU, memory, operating system, attached disks, and other properties. The worker nodes correspond to the Kubernetes `Node` resource, and are managed by a Kubernetes master that centrally controls and monitors all Kubernetes resources in the cluster. So when you deploy the resources for a containerized app, the Kubernetes master decides which worker node to deploy those resources on, accounting for the deployment requirements and available capacity in the cluster. Kubernetes resources include services, deployments, and pods.

Namespace
:   Kubernetes namespaces are a way to divide your cluster resources into separate areas that you can deploy apps and restrict access to, such as if you want to share the cluster with multiple teams. For example, system resources that are configured for you are kept in separate namespaces like `kube-system` or `ibm-system`. If you don't designate a namespace when you create a Kubernetes resource, the resource is automatically created in the `default` namespace.

Service
:   A service is a Kubernetes resource that groups a set of pods and provides network connectivity to these pods without exposing the actual private IP address of each pod. You can use a service to make your app available within your cluster or to the public internet.

Deployment
:   A deployment is a Kubernetes resource where you might specify information about other resources or capabilities that are required to run your app, such as services, persistent storage, or annotations. You document a deployment in a configuration YAML file, and then apply it to the cluster. The Kubernetes master configures the resources and deploys containers into pods on the worker nodes with available capacity.

:   Define update strategies for your app, including the number of pods that you want to add during a rolling update and the number of pods that can be unavailable at a time. When you perform a rolling update, the deployment checks whether the update is working and stops the rollout when failures are detected.

:   A deployment is just one type of workload controller that you can use to manage pods. For help choosing among your options, see [What type of Kubernetes objects can I make for my app?](/docs/openshift?topic=openshift-plan_deploy#object). For more information about deployments, see the [Kubernetes documentation](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/){: external}.
  
Pod
:   Every containerized app that is deployed into a cluster is deployed, run, and managed by a Kubernetes resource called a pod. Pods represent small deployable units in a Kubernetes cluster and are used to group the containers that must be treated as a single unit. Usually, each container is deployed in its own pod. However, an app might require a container and other helper containers to be deployed into one pod so that those containers can be addressed by using the same private IP address.

App
:   An app might refer to a complete app or a component of an app. You might deploy components of an app in separate pods or separate worker nodes. For more information, see [Planning app deployments](/docs/openshift?topic=openshift-plan_deploy) and [Developing Kubernetes-native apps](/docs/openshift?topic=openshift-app).

To dive deeper into Kubernetes, see the [Kubernetes documentation](https://kubernetes.io/docs/home/?path=users&persona=app-developer&level=foundational){: external}.
{: tip}


## What are containers?
{: #what-are-containers-overview}

Containers provide a standard way to package your application's code, configurations, and dependencies into a single unit that can run as a resource-isolated process on a compute server. To run your app in Kubernetes on {{site.data.keyword.openshiftlong_notm}}, you must first containerize your app by creating a container image that you store in a container registry.

Built on existing Linux container technology (LXC), the open source project that is named Docker defined templates for how to package software into standardized units, called containers, that include all the elements that an app needs to run. {{site.data.keyword.openshiftlong_notm}} uses `cri-o` as the container runtime to deploy containers from Docker container images into your cluster.


Image
:   A container image is the base for every container that you want to run. Container images are built from a Dockerfile, a text file that defines how to build the image and which build artifacts to include in it, such as the app, the app configuration, and its dependencies. Images are always built from other images, making them quick to configure. Let someone else do the bulk of the work on an image and then tweak it for your use.

Registry
:   An image registry is a place to store, retrieve, and share container images. Images that are stored in a registry can either be publicly available (public registry) or accessible by a small group of users (private registry). {{site.data.keyword.openshiftlong_notm}} offers public images, such as `ibmliberty`, that you can use to create your first containerized app. When it comes to enterprise applications, use a private registry like the one that is provided in {{site.data.keyword.cloud_notm}} to protect your images from being used by unauthorized users.

Container
:   Every container is created from an image. A container is a packaged app with all its dependencies so that the app can be moved between environments and run without changes. Unlike virtual machines, containers don't virtualize a device, its operating system, and the underlying hardware. Only the app code, run time, system tools, libraries, and settings are packaged inside the container. Containers run as isolated processes on Ubuntu compute hosts and share the host operating system and its hardware resources. This approach makes a container more lightweight, portable, and efficient than a virtual machine.


For more information, see the [Docker documentation](https://docs.docker.com/){: external}.
{: tip}



## What is {{site.data.keyword.redhat_openshift_notm}}?
{: #what-is-openshift-overview}

{{site.data.keyword.redhat_openshift_notm}} is a Kubernetes container platform that provides a trusted environment to run enterprise workloads. It extends the Kubernetes platform with built-in software to enhance app lifecycle development, operations, and security. With {{site.data.keyword.redhat_openshift_notm}}, you can consistently deploy your workloads across hybrid cloud providers and environments. For more information about the differences between the community Kubernetes and {{site.data.keyword.redhat_openshift_notm}} cluster offerings, see the [comparison table](/docs/openshift?topic=openshift-overview#openshift_kubernetes).

## What compute host infrastructure does {{site.data.keyword.openshiftlong_notm}} offer?
{: #what-compute-infra-is-offered}


With {{site.data.keyword.openshiftlong}}, you can create a cluster by using infrastructure from the following providers. All the worker nodes in a cluster must be from the same provider.


| Component | Description | 
| --- | --- |
| Overview | Create clusters on virtual servers in your own Virtual Private Cloud (VPC). |
| Supported container platforms | [{{site.data.keyword.redhat_openshift_notm}}]{: tag-red} or [Kubernetes]{: tag-blue} |
| Compute and worker node resources | Worker nodes are created as virtual machines by using either shared infrastructure or dedicated hosts. Unlike classic clusters, VPC cluster worker nodes on shared hardware don't appear in your infrastructure portal or a separate infrastructure bill. Instead, you manage all maintenance and billing activity for the worker nodes through {{site.data.keyword.openshiftlong_notm}}. Your worker node instances are connected to certain VPC instances that do reside in your infrastructure account, such as the VPC subnet or storage volumes. For dedicated hosts, the dedicated host price covers the vCPU, memory, and any [instance storage](/docs/vpc?topic=vpc-instance-storage) to be used by any workers placed on the host. Note that all Intel® x86-64 servers have Hyper-Threading enabled by default. For more information, see [Intel Hyper-Threading Technology](/docs/vpc?topic=vpc-profiles#vpc-intel-hyper-threading-technology). |
| Security | Clusters on shared hardware run in an isolated environment in the public cloud. Clusters on dedicated hosts do not run in a shared environment, instead only your clusters are present on your hosts. Network access control lists protect the subnets that provide the floating IPs for your worker nodes. |
| High availability | The master includes three replicas for high availability. Further, if you create your cluster in a multizone metro, the master replicas are spread across zones and you can also spread your worker pools across zones. |
| Reservations | Reservations aren't available for VPC. |
| Cluster administration | VPC clusters can't be reloaded or updated. Instead, use the [`worker replace --update` CLI](/docs/openshift?topic=openshift-kubernetes-service-cli#cli_worker_replace) or [API operation](https://containers.cloud.ibm.com/global/swagger-global-api/#/beta/replaceWorker){: external} to replace worker nodes that are outdated or in a troubled state. |
| Cluster networking | Unlike classic infrastructure, the worker nodes of your VPC cluster are attached to VPC subnets and assigned private IP addresses. The worker nodes are not connected to the public network, which instead is accessed through a public gateway, floating IP, or VPN gateway. For more information, see [Overview of VPC networking in {{site.data.keyword.openshiftlong_notm}}](/docs/openshift?topic=openshift-vpc-subnets#vpc_basics).|
| Apps and container platform | You can choose to create community Kubernetes or {{site.data.keyword.redhat_openshift_notm}} clusters to manage your containerized apps. Your app build processes don't differ because of the infrastructure provider, but how you expose the app does. |
| App networking | All pods that are deployed to a worker node are assigned a private IP address in the 172.30.0.0/16 range and are routed between worker nodes on the worker node private IP address of the private VPC subnet. To expose the app on the public network, you can create a Kubernetes `LoadBalancer` service, which provisions a VPC load balancer and public hostname address for your worker nodes. For more information, see [Exposing apps with VPC load balancers](/docs/openshift?topic=openshift-vpc-lbaas). |
| Storage | You can choose from non-persistent and persistent storage solutions such as file, block, object, and software-defined storage. For more information, see [Planning highly available persistent storage](/docs/openshift?topic=openshift-storage-plan). |
| User access | You can use [{{site.data.keyword.cloud_notm}} IAM access policies](/docs/vpc?topic=vpc-iam-getting-started) to authorize users to create infrastructure, manage your cluster, and access cluster resources. The cluster can be in a different resource group than the VPC. |
| Integrations | VPC supports a select list of supported {{site.data.keyword.cloud_notm}} services, add-ons, and third-party integrations. For a list, see [Supported {{site.data.keyword.cloud_notm}} and third-party integrations](/docs/openshift?topic=openshift-supported_integrations). |
| Locations and versions | VPC clusters are available worldwide in the [multizone location](/docs/openshift?topic=openshift-regions-and-zones#zones-vpc).
| Service interface | VPC clusters are supported by the [next version (`v2`) of the {{site.data.keyword.containerlong_notm}} API](/docs/openshift?topic=openshift-cs_api_install), and you can manage your VPC clusters through the same CLI and console as classic clusters.| 
| Service compliance | See the VPC section in [What standards does the service comply to?](/docs/openshift?topic=openshift-faqs#standards).
| Service limitations | See [Service limitations](/docs/openshift?topic=openshift-limitations#tech_limits). For VPC-specific limitations in {{site.data.keyword.openshiftlong_notm}}, see [VPC cluster limitations](/docs/openshift?topic=openshift-limitations#ks_vpc_gen2_limits). For general VPC infrastructure provider limitations, see [Limitations](/docs/vpc?topic=vpc-limitations).  |
{: class="simple-tab-table"}
{: caption="Table 1. Infrastructure overview" caption-side="bottom"}
{: #infra-1}
{: tab-title="VPC"}
{: tab-group="infra-table"}



| Component | Description | 
| --- | --- |
| Overview | Create clusters on your own hardware, {{site.data.keyword.cloud_notm}} Classic or VPC, or on virtual servers in another cloud provider like AWS or Azure. |
| Supported container platforms | [{{site.data.keyword.redhat_openshift_notm}}]{: tag-red} |
| Compute and worker node resources | Worker nodes can be virtual machines using either shared infrastructure or dedicated hosts, or even bare metal servers. You manage maintenance and billing activity for the worker nodes through your host infrastructure provider whether that is {{site.data.keyword.cloud_notm}}, your own on-premises hardware, or another cloud provider. You also manage billing through {{site.data.keyword.cloud_notm}}. For more information about pricing, see [What am I charged for when I use {{site.data.keyword.satellitelong_notm}}?](/docs/satellite?topic=satellite-faqs#pricing). |
| Security | See [Security and compliance](/docs/satellite?topic=satellite-compliance). |
| High availability | See [About high availability and recover](/docs/satellite?topic=satellite-ha). |
| Reservations | Reservations aren't available for {{site.data.keyword.satelliteshort}}. |
| Cluster administration | See [Updating hosts that are assigned as worker nodes](/docs/satellite?topic=satellite-host-update-workers). | 
| Cluster networking | If you attach {{site.data.keyword.cloud_notm}} Classic or VPC hosts to your location, refer to those descriptions. |
| Apps and container platform | You can create [{{site.data.keyword.redhat_openshift_notm}} clusters](/docs/openshift?topic=openshift-faqs#container_platforms) to manage your containerized apps. Your app build processes don't differ because of the infrastructure provider, but how you expose the app does. For more information, see [Choosing an app exposure service](/docs/openshift?topic=openshift-cs_network_planning). |
| App networking | All pods that are deployed to a worker node are assigned a private IP address in the 172.30.0.0/16 range by default. You can avoid subnet conflicts with the network that you use to connect to your location by specifying a custom subnet CIDR that provides the private IP addresses for your pods. To expose an app, see [Exposing apps in {{site.data.keyword.satelliteshort}} clusters](/docs/openshift?topic=openshift-sat-expose-apps). |
| Storage | Bring your own storage drivers or deploy one of the supported storage templates. For more information, see [Understanding {{site.data.keyword.satelliteshort}} storage](/docs/satellite?topic=satellite-storage-template-ov). | 
| User access | You can use {{site.data.keyword.cloud_notm}} IAM access policies to authorize users to create {{site.data.keyword.cloud_notm}} infrastructure, manage your cluster, and access cluster resources. For more information, see [Managing access overview](/docs/satellite?topic=satellite-iam). You can also further control access to your host infrastructure in policies provided by your infrastructure provider.|
| Integrations | For cluster integrations, see [Supported {{site.data.keyword.cloud_notm}} and third-party integrations](/docs/openshift?topic=openshift-supported_integrations). For supported {{site.data.keyword.satelliteshort}} service integrations, see [Supported {{site.data.keyword.satelliteshort}} {{site.data.keyword.cloud_notm}} services](/docs/satellite?topic=satellite-managed-services).
| Locations and versions | Clusters are managed from one of the [supported {{site.data.keyword.cloud_notm}} locations](/docs/satellite?topic=satellite-sat-regions). However, you can deploy worker nodes to your own location, an {{site.data.keyword.cloud_notm}} data center, or another cloud provider. For more information see [Understanding locations and hosts](/docs/satellite?topic=satellite-location-host). |
| Service interface | {{site.data.keyword.satelliteshort}} are supported by the global [API](https://containers.cloud.ibm.com/global/swagger-global-api/) [{{site.data.keyword.containerlong_notm}}, the {{site.data.keyword.openshiftlong_notm}} [CLI](/docs/openshift?topic=openshift-cli-install) and the {{site.data.keyword.satelliteshort}} [CLI](/docs/satellite?topic=satellite-cli-install). You can also manage your clusters from the [console](https://cloud.ibm.com/satellite/clusters). |
| Service compliance | For clusters, see [What standards does the service comply to?](/docs/openshift?topic=openshift-faqs#standards). For {{site.data.keyword.satelliteshort}}, see [Security and compliance](/docs/satellite?topic=satellite-compliance). |
| Service limitations | See [Limitations, default settings, and usage requirements](/docs/satellite?topic=satellite-requirements). |
{: class="simple-tab-table"}
{: caption="Table 1. Infrastructure overview" caption-side="bottom"}
{: #infra-2}
{: tab-title="{{site.data.keyword.satelliteshort}}"}
{: tab-group="infra-table"}




| Component | Description | 
| --- | --- |
| Overview | Create clusters in a classic compute, networking, and storage environment in IBM Cloud infrastructure. |
| Supported container platforms | [{{site.data.keyword.redhat_openshift_notm}}]{: tag-red} or [Kubernetes]{: tag-blue} |
| Compute and worker node resources | [Virtual](/docs/openshift?topic=openshift-planning_worker_nodes#vm), [bare metal](/docs/openshift?topic=openshift-planning_worker_nodes#bm), and [software-defined storage](/docs/openshift?topic=openshift-planning_worker_nodes#sds) machines are available for your worker nodes. Your worker node instances reside in your IBM Cloud infrastructure account, but you can manage them through {{site.data.keyword.openshiftlong_notm}}. You own the worker node instances.|
| Security | Built-in security features that help you protect your cluster infrastructure, isolate resources, and ensure security compliance. For more information, see the [classic Network Infrastructure documentation](/docs/cloud-infrastructure?topic=cloud-infrastructure-compare-infrastructure). |
| High availability | For both classic and VPC clusters, the master includes three replicas for high availability. Further, if you create your cluster in a multizone metro, the master replicas are spread across zones and you can also spread your worker pools across zones. For more information, see [High availability for {{site.data.keyword.openshiftlong_notm}}](/docs/openshift?topic=openshift-ha_clusters). |
| Reservations | [Create a reservation](/docs/openshift?topic=openshift-reservations) with contracts for 1 or 3 year terms for classic worker nodes to lock in a reduced cost for the life of the contract. Typical savings range between 30-50% compared to regular worker node costs. | 
| Cluster administration | Classic clusters support the entire set of `v1` API operations, such as resizing worker pools, reloading worker nodes, and updating masters and worker nodes across major, minor, and patch versions. When you delete a cluster, you can choose to remove any attached subnet or storage instances. | 
| Cluster networking | Your worker nodes are provisioned on private VLANs that provide private IP addresses to communicate on the private IBM Cloud infrastructure network. For communication on the public network, you can also provision the worker nodes on a public VLAN. Communication to the cluster master can be on the public or private cloud service endpoint. For more information, see [Understanding VPC cluster network basics](/docs/openshift?topic=openshift-plan_vpc_basics) or [Understanding Classic cluster network basics](/docs/openshift?topic=openshift-plan_basics). |
| Apps and container platform | You can choose to create [community Kubernetes or {{site.data.keyword.redhat_openshift_notm}} clusters](/docs/openshift?topic=openshift-faqs#container_platforms) to manage your containerized apps. Your app build processes don't differ because of the infrastructure provider, but how you expose the app does. For more information, see [Choosing an app exposure service](/docs/openshift?topic=openshift-cs_network_planning). |
| App networking | All pods that are deployed to a worker node are assigned a private IP address in the 172.30.0.0/16 range and are routed between worker nodes on the worker node private IP address of the private VLAN. To expose the app on the public network, your cluster must have worker nodes on the public VLAN. Then, you can create a NodePort, LoadBalancer (NLB), or Ingress (ALB) service. For more information, see [Planning in-cluster and external networking for apps](/docs/openshift?topic=openshift-cs_network_planning).
| Storage | You can choose from non-persistent and persistent storage solutions such as file, block, object, and software-defined storage. For more information, see [Planning highly available persistent storage](/docs/openshift?topic=openshift-storage-plan). |
| User access | To create classic infrastructure clusters, you must set up [infrastructure credentials](/docs/openshift?topic=openshift-access-creds) for each region and resource group. To let users manage the cluster, use [{{site.data.keyword.cloud_notm}} IAM platform access roles](/docs/openshift?topic=openshift-iam-platform-access-roles). To grant users access to cluster resources, use [{{site.data.keyword.cloud_notm}} IAM service access roles](/docs/openshift?topic=openshift-iam-platform-access-roles), which correspond with Kubernetes RBAC roles. |
| Integrations | You can extend your cluster and app capabilities with a variety of {{site.data.keyword.cloud_notm}} services, add-ons, and third-party integrations. For a list, see [Supported {{site.data.keyword.cloud_notm}} and third-party integrations](/docs/openshift?topic=openshift-supported_integrations). |
| Locations and versions | Classic clusters are available in multizone and single zone locations [worldwide](/docs/openshift?topic=openshift-regions-and-zones#locations). |
| Service interface | Classic clusters are fully supported in the {{site.data.keyword.containershort_notm}} [`v1` API](https://containers.cloud.ibm.com/global/swagger-global-api/#/){: external}, [CLI](/docs/openshift?topic=openshift-kubernetes-service-cli), and [console](https://cloud.ibm.com/kubernetes/clusters).|
| Service compliance | See the classic section in [What standards does the service comply to?](/docs/openshift?topic=openshift-faqs#standards). |
| Service limitations | See [Service limitations](/docs/openshift?topic=openshift-limitations#tech_limits). Feature-specific limitations are documented by section. |
{: class="simple-tab-table"}
{: caption="Table 1. Infrastructure overview" caption-side="bottom"}
{: #infra-3}
{: tab-title="Classic"}
{: tab-group="infra-table"}



## What are the benefits of using the service?
{: #benefits}



With {{site.data.keyword.openshiftlong_notm}}, your developers have a fast and secure way to containerize and deploy enterprise workloads in Kubernetes clusters. {{site.data.keyword.redhat_openshift_notm}} clusters build on Kubernetes container orchestration that offers consistency and flexibility for your development lifecycle operations.

Your {{site.data.keyword.redhat_openshift_notm}} workloads can scale across IBM’s global footprint of data centers and multizone regions. At the same time, you’re able to uniformly monitor, log, and secure apps. Because IBM manages the service, you can focus on innovating with high-value {{site.data.keyword.cloud_notm}} services and middleware, such as AI and analytics. You also have access to Red Hat packaged open-source tools, including your favorite app runtimes, frameworks, databases, and more.

Ready to get started? Try out the [creating a {{site.data.keyword.openshiftlong_notm}} cluster tutorial](/docs/openshift?topic=openshift-openshift_tutorial).


Choice of container platform provider
:   Deploy clusters with **{{site.data.keyword.redhat_openshift_notm}}** or community **Kubernetes** installed as the container platform orchestrator.
:   Choose the developer experience that fits your company, or run workloads across both {{site.data.keyword.redhat_openshift_notm}} or community Kubernetes clusters.
:   Built-in integrations from the {{site.data.keyword.cloud_notm}} console to the Kubernetes dashboard or {{site.data.keyword.redhat_openshift_notm}} web console.
:   Single view and management experience of all your {{site.data.keyword.redhat_openshift_notm}} or community Kubernetes clusters from {{site.data.keyword.cloud_notm}}. For more information, see Comparison between [{{site.data.keyword.redhat_openshift_notm}}](#openshift_kubernetes) and community Kubernetes clusters.


Single-tenant Kubernetes clusters with compute, network, and storage infrastructure isolation
:  Create your own customized infrastructure that meets the requirements of your organization.
:  Choose between [infrastructure providers](/docs/openshift?topic=openshift-overview#what-compute-infra-is-offered).
:   Provision a dedicated and secured {{site.data.keyword.redhat_openshift_notm}} master, worker nodes, virtual networks, and storage by using the resources provided by IBM Cloud infrastructure.
:   Fully managed Kubernetes master that is continuously monitored and updated by {{site.data.keyword.IBM_notm}} to keep your cluster available.
:   Option to provision worker nodes as bare metal servers for compute-intensive workloads such as data, GPU, and AI.
:   Store persistent data, share data between Kubernetes pods, and restore data when needed with the integrated and secure volume service.
:   Benefit from full support for all native Kubernetes APIs.

Multizone clusters to increase high availability
:   Easily manage worker nodes of the same flavor (CPU, memory, virtual or physical) with worker pools.
:   Guard against zone failure by spreading nodes evenly across select multizones and by using anti-affinity pod deployments for your apps.
:   Decrease your costs by using multizone clusters instead of duplicating the resources in a separate cluster.
:   Benefit from automatic load balancing across apps with the multizone load balancer (MZLB) that is set up automatically for you in each zone of the cluster.


Highly available masters
:   Reduce cluster downtime such as during master updates with highly available masters that are provisioned automatically when you create a cluster.
:   Spread your masters across zones in a [multizone cluster](/docs/openshift?topic=openshift-ha_clusters#mz-clusters) to protect your cluster from zonal failures.

Image security compliance with Vulnerability Advisor
:   Set up your own repo in a secured Docker private image registry where images are stored and shared by all users in the organization.
:   Benefit from automatic scanning of images in your private {{site.data.keyword.cloud_notm}} registry.
:   Review recommendations specific to the operating system used in the image to fix potential vulnerabilities.

Continuous monitoring of the cluster health
:   Use the cluster dashboard to quickly see and manage the health of your cluster, worker nodes, and container deployments.
:   Find detailed consumption metrics by using {{site.data.keyword.mon_full}} and quickly expand your cluster to meet work loads.
:   Review logging information by using {{site.data.keyword.la_full}} to see detailed cluster activities.

Secure exposure of apps to the public
:   Choose between a public IP address, an {{site.data.keyword.IBM_notm}} provided route, or your own custom domain to access services in your cluster from the internet.

{{site.data.keyword.cloud_notm}} service integration
:   Add extra capabilities to your app through the integration of {{site.data.keyword.cloud_notm}} services, such as {{site.data.keyword.watson}} APIs, Blockchain, data services, or Internet of Things.


## Comparison between {{site.data.keyword.redhat_openshift_notm}} and Kubernetes clusters
{: #openshift_kubernetes}

Both {{site.data.keyword.openshiftlong_notm}} and {{site.data.keyword.containerlong_notm}} clusters are production-ready container platforms that are tailored for enterprise workloads. The following table compares and contrasts some common characteristics that can help you choose which container platform is best for your use case.
{: shortdesc}

|Characteristics|Kubernetes clusters|{{site.data.keyword.redhat_openshift_notm}} clusters|
|---------------|-------------|-----------------|
|Complete cluster management experience through the {{site.data.keyword.containerlong_notm}} automation tools (API, CLI, console)|Yes|Yes|
|Worldwide availability in single and multizones|Yes|Yes|
|Consistent container orchestration across hybrid cloud providers|Yes|Yes|
|Access to {{site.data.keyword.cloud_notm}} services such as AI|Yes|Yes|
|Software-defined storage Portworx solution available for multizone data use cases|Yes|Yes|
|Create a cluster in an IBM Virtual Private Cloud (VPC)|Yes|Yes|
|Latest Kubernetes distribution|Yes| |
|Scope {{site.data.keyword.cloud_notm}} IAM access policies to access groups for service access roles that sync to cluster RBAC |Yes| |
|Classic infrastructure cluster on only the private network|Yes| |
| GPU bare metal worker nodes | Yes | Yes |
|Integrated IBM Cloud Paks and middleware| |Yes|
|Built-in container image streams, builds, and tooling ([read more](https://blog.cloudowski.com/articles/why-managing-container-images-on-openshift-is-better-than-on-kubernetes/){: external})| |Yes|
|Integrated CI/CD with Jenkins| |Yes|
|Stricter app security context set up by default| |Yes|
|Simplified Kubernetes developer experience, with an app console that is suited for beginners| |Yes|
|Supported operating system| [Kubernetes version information](/docs/containers?topic=containers-cs_versions). | [{{site.data.keyword.redhat_openshift_notm}} version information](/docs/openshift?topic=openshift-openshift_versions). |
|Preferred external traffic networking| Ingress | Router |
|Secured routes encrypted with {{site.data.keyword.hscrypto}} | | Yes |
{: caption="Characteristics of Kubernetes and {{site.data.keyword.redhat_openshift_notm}} clusters" caption-side="bottom"}



## Comparison between clusters that run in {{site.data.keyword.cloud_notm}} and standard OCP
{: #compare_ocp}

Because {{site.data.keyword.openshiftlong_notm}} is a managed service, many of the {{site.data.keyword.openshiftlong}} components and global settings that you manually set up in OpenShift Container Platform are set up for you by default in {{site.data.keyword.openshiftlong_notm}}. Review the following differences between {{site.data.keyword.openshiftlong_notm}} clusters and a standard installation of OpenShift Container Platform on your own infrastructure. You can also review the [service architecture](/docs/openshift?topic=openshift-service-architecture) for an overview of how {{site.data.keyword.redhat_openshift_notm}} components are set up in the cluster master and worker nodes, or the [global settings](/docs/openshift?topic=openshift-service-settings#global-settings) that you can or can't configure.
{: shortdesc}

|Characteristics|Standard OCP|{{site.data.keyword.openshiftlong_notm}}|
|---------------|----------------------|----------------------------------------|
| Cluster master (control plane) | You set up control plane components like the API server and etcd on machines that get the `master` role. You can modify the control plane components, but keep in mind that you are responsible for backing up, restoring, and making control plane data highly available. | IBM sets up the master, manages the control plane components, and automatically applies master patch updates for you. The masters are highly available and backed up automatically.|
| Compute machines (worker nodes) | You create your own compatible compute machines, set up compatible network connectivity, SSH into the machines, install OCP, and register the machines as worker nodes in the cluster. Your machines might be installer-provisioned infrastructure (IPI) for a guided setup, or user-provisioned infrastructure (UPI) for more control and subsequent administration on your end. You are responsible for maintaining and updating the worker nodes. You can install updates from the {{site.data.keyword.redhat_openshift_notm}} web console. | You select the flavor of worker nodes that you want to add to your cluster, and IBM automatically connects the worker nodes to the cluster and installs OCP. In this sense, the installation is similar to IPI for you because you don't have to manage all the infrastructure and network settings. IBM also provides patch updates that you can choose to apply to your worker nodes, from the {{site.data.keyword.cloud_notm}} interface (not the {{site.data.keyword.redhat_openshift_notm}} web console). SSH is disabled for added security. |
| OCP versions and patch updates | You are responsible for updating the underlying infrastructure for the master and worker nodes. You can use the {{site.data.keyword.redhat_openshift_notm}} web console to update OCP versions. | IBM automatically applies updates to the master, and provides version updates and security patch updates for the worker nodes. You choose when to apply these updates to your worker nodes, from the {{site.data.keyword.cloud_notm}} interface (not the {{site.data.keyword.redhat_openshift_notm}} web console). Supported versions might vary from standard OpenShift Container Platform.|
| Autoscaling compute machines | You can set up a `ClusterAutoscaler` resource. | You can set up the [cluster autoscaler plug-in](/docs/openshift?topic=openshift-cluster-scaling-install-addon). |
| Worker node operating system | CoreOS or RHEL | For a list of supported operating systems by cluster version, see [{{site.data.keyword.openshiftlong_notm}} version information](/docs/openshift?topic=openshift-openshift_versions). |
| Support | Provided per the terms of your Red Hat subscription or cloud provider. You can use the `oc adm must-gather` tool to help gather information. | Provided by [{{site.data.keyword.cloud_notm}} Support](https://www.ibm.com/cloud/support){: external}. You can use the `oc adm must-gather` tool, or the [Diagnostics and Debug Tool](/docs/openshift?topic=openshift-debug-tool) to help gather information. |
| {{site.data.keyword.redhat_openshift_notm}} web console | You set up and can configure or disable the {{site.data.keyword.redhat_openshift_notm}} web console. | The {{site.data.keyword.redhat_openshift_notm}} web console is set up for you. You can't configure or disable the web console. IBM also provides the [{{site.data.keyword.redhat_openshift_notm}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external} to manage your cluster infrastructure. |
| Authentication | An OAuth server is provided, but you configure the token settings and identity provider to control access to the cluster. You also manage RBAC to control user access within the cluster. | IBM automatically sets up the OAuth server to use {{site.data.keyword.cloud_notm}} IAM. You can't change the identity provider. {{site.data.keyword.cloud_notm}} IAM is also set up to [automatically sync to RBAC](/docs/openshift?topic=openshift-iam-platform-access-roles) so that you can use IAM to manage access to and within the cluster. |
| Container network for clusters | The cluster network operator sets up the SDN container network interface (CNI) plug-in. You can change the CNI plug-in, configure multiple networks, or attach a hardware network such as single root I/O virtualization (SR-IOV). | Calico is set up for you. You can't change the CNI plug-in, configure multiple networks, or attach a hardware network.|
| Ingress | You can use the Ingress operator to set up one or more HAProxy-based Ingress controllers. You can route traffic to your apps by specifying `Route` or `Ingress` resources. | When you create a cluster, a default Ingress subdomain is set up for you. One HAProxy-based router is set up for each Ingress controller, and one router service is automatically created in each zone that you have worker nodes in. You can route traffic to your apps by specifying `Route` or `Ingress` resources. For more information, see [About Ingress in {{site.data.keyword.redhat_openshift_notm}} version 4](/docs/openshift?topic=openshift-ingress-about-roks4). |
| Storage | You must set up persistent volumes to be backed up by a storage provider. OpenShift Data Foundation is available. | IBM automatically sets up storage providers such as {{site.data.keyword.cloud_notm}} File and Block. OpenShift Data Foundation is available. For supported storage options, see [Planning highly available persistent storage](/docs/openshift?topic=openshift-storage-plan). |
| Image registry | The cluster is set up with an internal registry to pull images. If your cluster has public network access, you can pull images automatically from Docker Hub. To pull images from other registries, you must set up image pull secrets. You set up the internal registry to back up images to a cloud storage provider. Stored images are not available across clusters. | The internal registry is set up to back up images automatically to a bucket in your {{site.data.keyword.cos_full_notm}} instance. Your cluster has image pull secrets automatically set up to pull images from default registries, including {{site.data.keyword.registrylong_notm}}. You can also set up the internal registry to work with {{site.data.keyword.registrylong_notm}}, which your cluster is also automatically set up to pull images from. For more information, see [Setting up an image registry](/docs/openshift?topic=openshift-registry). |
| Operators and OperatorHub | OpenShift Container Platform sets up many operators to manage default components for the cluster. You can also use the OperatorHub to install other operators such as from 3rd-party providers. | IBM sets up many of the same operators as OCP to manage default component for the cluster. However, because IBM manages the master and provides you with {{site.data.keyword.cloud_notm}} APIs to manage your cloud infrastructure, some operators, such as the machine set operator and other components as noted in this table, are not set up or configurable. You can also use the OperatorHub to [install other operators](/docs/openshift?topic=openshift-operators) such as from 3rd-party providers. Note that operators that you install or create are not supported by IBM, and might come with their own support terms and pricing.|
| Projects, builds, and apps | OpenShift Container Platform provides tools such as projects, build configurations, and the internal registry that you can use to deploy your apps while following a cloud-native, continuous integration and continuous delivery (CI/CD) methodology. | {{site.data.keyword.openshiftlong_notm}} clusters come with all the same configurable project and build components as OCP clusters. You can also choose to integrate your cluster with {{site.data.keyword.cloud_notm}} services like [{{site.data.keyword.contdelivery_short}}](/docs/openshift?topic=openshift-cicd). |
| Cluster health | You can also set up logging, monitoring, and metering tools by installing and configuring various operators. These solutions are cluster-specific and not highly available unless you back them up. | Your clusters feature one-click integrations with {{site.data.keyword.la_full_notm}} and {{site.data.keyword.mon_full_notm}} for enterprise-grade, persistent monitoring and logging solutions across clusters. You can also install the logging and monitoring operators as with standard OCP, but you might have to adjust the configuration settings. For more information, see [Logging and monitoring cluster health](/docs/openshift?topic=openshift-health). |
| Migrating clusters | You can use the cluster migrator operator to migrate clusters from one major version to another. Migration requires separate clusters; you can't update a cluster from one major version to another. Various open source tools might be used, but are not officially supported. | As with standard OpenShift Container Platform, you can't update a cluster from one major version to another. If you use a third-party open source tool such as the [cluster migrator operator](https://github.com/migtools/mig-operator){: external}, the tool is not supported by IBM and might have limitations such as the migration UI being unavailable. |
| Container-native virtualization | You can set up [container-native virtualization add-on](https://docs.openshift.com/container-platform/4.13/virt/about-virt.html){: external} on bare metal machines, but not on virtual machines. Container-native virtualization is not supported by IBM. If you experience issues, you are responsible for resolving the issues and any impact to your workloads. |
| Serverless workloads | You can set up [{{site.data.keyword.redhat_openshift_notm}} Serverless](https://www.redhat.com/en/topics/microservices/why-choose-openshift-serverless){: external}. | You can also set up {{site.data.keyword.redhat_openshift_notm}} Serverless. |
| Service mesh | You can set up the [{{site.data.keyword.redhat_openshift_notm}} Service Mesh](https://docs.openshift.com/container-platform/4.14/service_mesh/v1x/installing-ossm.html){: external}. | You can also set up the {{site.data.keyword.redhat_openshift_notm}} Service Mesh, but you must [apply a network policy](https://gist.githubusercontent.com/kitch/39c504a2ed9e381c2aadea436d5b52e4/raw/d8efa69f41d41425b16bb363a881a98d40d3708c/mesh-policy.yaml){: external} for the service mesh ingress to work.|
| API and CLI tools | OpenShift Container Platform clusters are set up with access to Kubernetes and {{site.data.keyword.redhat_openshift_notm}} API resources. You can also install command line tools such as `oc` and `odo`. | {{site.data.keyword.openshiftlong_notm}} clusters come with the same capabilities to use the Kubernetes and {{site.data.keyword.redhat_openshift_notm}} API and CLI tools. Additionally, you can use the {{site.data.keyword.cloud_notm}} [API](/docs/openshift?topic=openshift-cs_api_install) and [CLI](/docs/openshift?topic=openshift-cli-install) tools to manage your cluster infrastructure and integrate other cloud services with your cluster.|
{: caption="Comparison between clusters that run in {{site.data.keyword.cloud_notm}} and standard OCP" caption-side="bottom"}


## Moving your workloads to {{site.data.keyword.cloud_notm}}
{: #cloud_workloads}

You have lots of reasons to move your workloads to {{site.data.keyword.cloud_notm}}: reducing total cost of ownership, increasing high availability for your apps in a secure and compliant environment, scaling up and down in respond to your user demand, and many more. {{site.data.keyword.openshiftlong_notm}} combines container technology with open source tools, such as Kubernetes so that you can build a cloud-native app that can migrate across different cloud environments, avoiding vendor lock-in.
{: shortdesc}

But how do you get to the cloud? What are your options along the way? And how do you manage your workloads after you get there?

Use this page to learn some strategies for your Kubernetes deployments on {{site.data.keyword.openshiftlong_notm}}. And engage with the team on [Slack](https://ibm-cloud-success.slack.com){: external}.

Not on slack yet? [Request an invite!](https://cloud.ibm.com/kubernetes/slack){: external}
{: tip}

The following table provides some examples of what types of workloads that users typically move to the various types of clouds. You might also choose a hybrid approach where you have clusters that run in both environments.


| Workload | {{site.data.keyword.openshiftlong_notm}} off-prem | on-prem |
| --- | --- | --- |
| DevOps enablement tools | Yes | |
| Developing and testing apps | Yes | |
| Apps that shift dramatically in demand and need to scale rapidly | Yes | |
| Business apps such as CRM, HCM, ERP, and E-commerce | Yes | |
| Collaboration and social tools such as email | Yes | |
| RHEL workloads | Yes | |
| Bare metal | Yes | Yes |
| GPU compute resources | Yes | Yes |
| PCI and HIPAA-compliant workloads | Yes | Yes |
| Legacy apps with platform and infrastructure constraints and dependencies | | Yes |
| Proprietary apps with strict designs, licensing, or heavy regulations | | Yes |
{: caption="{{site.data.keyword.cloud_notm}} implementations that support your workloads" caption-side="bottom"}

Ready to run workloads off-premises in {{site.data.keyword.openshiftlong_notm}}?
:   Great! You're already in the public cloud documentation. Keep reading for more strategy ideas, or hit the ground running by [creating a cluster now](/docs/openshift?topic=openshift-getting-started).

Want to run workloads in both on-premises and off-premises clouds?
:   Explore [{{site.data.keyword.satellitelong_notm}}](/docs/satellite?topic=satellite-faqs) to extend the flexibility and scalability of {{site.data.keyword.cloud_notm}} into your on-premises, edge, or other cloud provider environments.


## What kind of apps can I run? Can I move existing apps, or do I need to develop new apps?
{: #app_kinds}

Your containerized app must be able to run on one of the [supported operating systems](/docs/openshift?topic=openshift-openshift_versions) for your cluster version. You also want to consider the statefulness of your app. For more information about the kinds of apps that can run in {{site.data.keyword.openshiftlong_notm}}, see [Planning app deployments](/docs/openshift?topic=openshift-plan_deploy#app_types).

If you already have an app, you can [migrate it to {{site.data.keyword.openshiftlong_notm}}](/docs/openshift?topic=openshift-plan_deploy#migrate_containerize). If you want to develop a new app, check out the [guidelines for developing stateless, cloud-native apps](/docs/openshift?topic=openshift-plan_deploy#12factor).


## What skills should I have before I move my apps to a cluster?
{: #knowledge}

{{site.data.keyword.redhat_openshift_notm}} is designed to provide capabilities to two main personas, the cluster admin and the app developer. Each persona uses different technical skills to successfully run and deploy apps to a cluster.


What are a cluster admin's main tasks and technical knowledge?
:   As a cluster admin, you are responsible to set up, operate, secure, and manage the {{site.data.keyword.cloud_notm}} infrastructure of your cluster. Typical tasks include:
    - Size the cluster to provide enough capacity for your workloads.
    - Design a cluster to meet the high availability, disaster recovery, and compliance standards of your company.
    - Secure the cluster by setting up user permissions and limiting actions within the cluster to protect your compute resources, your network, and data.
    - Plan and manage network communication between infrastructure components to ensure network security, segmentation, and compliance.
    - Plan persistent storage options to meet data residency and data protection requirements.

The cluster admin persona must have a broad knowledge that includes compute, network, storage, security, and compliance. In a typical company, this knowledge is spread across multiple specialists, such as System Engineers, System Administrators, Network Engineers, Network Architects, IT Managers, or Security and Compliance Specialists. Consider assigning the cluster admin role to multiple people in your company so that you have the required knowledge to successfully operate your cluster. For more information, see the [Learning path for administrators](/docs/openshift?topic=openshift-learning-path-admin).

What are an app developer's main tasks and technical skills?
:   As a developer, you design, create, secure, deploy, test, run, and monitor cloud-native, containerized apps in an {{site.data.keyword.redhat_openshift_notm}} cluster. To create and run these apps, you must be familiar with the concept of microservices, the [12-factor app](/docs/openshift?topic=openshift-plan_deploy#12factor) guidelines, [Docker and containerization principles](https://www.docker.com/){: external}, and available [{{site.data.keyword.redhat_openshift_notm}} deployment options](/docs/openshift?topic=openshift-plan_deploy). For more information, see the [Learning path for developers](/docs/openshift?topic=openshift-learning-path-dev).

{{site.data.keyword.redhat_openshift_notm}} and {{site.data.keyword.openshiftlong_notm}} provide multiple options for how to [expose an app and keep an app private](/docs/containers?topic=containers-cs_network_planning), [add persistent storage](/docs/openshift?topic=openshift-storage-plan), [integrate other services](/docs/openshift?topic=openshift-ibm-3rd-party-integrations), and how you can [secure your workloads and protect sensitive data](/docs/openshift?topic=openshift-security#container). Before you move your app to a cluster in {{site.data.keyword.openshiftlong_notm}}, verify that you can run your app as a containerized app on the supported operating system and that {{site.data.keyword.redhat_openshift_notm}} and {{site.data.keyword.openshiftlong_notm}} provide the capabilities that your workload needs.





## Related resources
{: #kubernetes-resources}

Review how you can learn about Kubernetes concepts and the terminology.
{: shortdesc}


* Familiarize yourself with the product by completing the [Creating clusters tutorial](/docs/openshift?topic=openshift-openshift_tutorial).
* Learn how Kubernetes and {{site.data.keyword.openshiftlong_notm}} work together by completing this [course](https://cognitiveclass.ai/courses/kubernetes-course){: external}.


