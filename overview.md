---

copyright: 
  years: 2014, 2022
lastupdated: "2022-04-07"

keywords: openshift

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Overview
{: #roks-overview}

Learn more about [{{site.data.keyword.openshiftlong}}](https://www.ibm.com/cloud/openshift){: external}, its capabilities, and the options that are available to you to customize the cluster to your needs.
{: shortdesc}


## Understanding {{site.data.keyword.openshiftlong_notm}}
{: #service-concepts}

Review frequently asked questions and key technologies that {{site.data.keyword.openshiftlong_notm}} uses.
{: shortdesc}

**What is {{site.data.keyword.openshiftlong_notm}} and how does it work?**

{{site.data.keyword.openshiftlong_notm}} is a managed offering to create your own {{site.data.keyword.redhat_openshift_notm}} cluster of compute hosts to deploy and manage containerized apps on {{site.data.keyword.cloud_notm}}. {{site.data.keyword.openshiftlong_notm}} provides intelligent scheduling, self-healing, horizontal scaling, service discovery and load balancing, automated rollouts and rollbacks, and secret and configuration management for your apps. Combined with an intuitive user experience, built-in security and isolation, and advanced tools to secure, manage, and monitor your cluster workloads, you can rapidly deliver highly available and secure containerized apps in the public cloud.

**What is Kubernetes?**

Kubernetes is an open source platform for managing containerized workloads and services across multiple hosts, and offers management tools for deploying, automating, monitoring, and scaling containerized apps with minimal to no manual intervention. For an overview of key Kubernetes concepts, see [Kubernetes clusters](#kubernetes_basics). To dive deeper into Kubernetes, see the [Kubernetes documentation](https://kubernetes.io/docs/home/?path=users&persona=app-developer&level=foundational){: external}.

**What are containers?**

Containers provide a standard way to package your application's code, configurations, and dependencies into a single unit that can run as a resource-isolated process on a compute server. To run your app in Kubernetes on {{site.data.keyword.openshiftlong_notm}}, you must first containerize your app by creating a container image that you store in a container registry. For an overview of key Docker concepts and benefits, see [Docker containers](#docker_containers). To dive deeper into Docker, see the [Docker documentation](https://docs.docker.com/){: external}.

**What is {{site.data.keyword.redhat_openshift_notm}}?**

{{site.data.keyword.redhat_openshift_notm}} is a Kubernetes container platform that provides a trusted environment to run enterprise workloads. It extends the Kubernetes platform with built-in software to enhance app lifecycle development, operations, and security. With {{site.data.keyword.redhat_openshift_notm}}, you can consistently deploy your workloads across hybrid cloud providers and environments. For more information about the differences between the community Kubernetes and {{site.data.keyword.redhat_openshift_notm}} cluster offerings, see the [comparison table](/docs/openshift?topic=openshift-cs_ov#openshift_kubernetes).

**What compute host infrastructure does the service offer?**

With {{site.data.keyword.openshiftlong_notm}}, you can create your cluster of compute hosts on classic {{site.data.keyword.cloud_notm}} infrastructure or VPC infrastructure.

[Classic clusters](/docs/containers?topic=containers-getting-started) are created on your choice of virtual or bare metal worker nodes that are connected to VLANs. If you require additional local disks, you can also choose one of the bare metal flavors that are designed for software-defined storage solutions, such as Portworx. Depending on the level of hardware isolation that you need, virtual worker nodes can be set up as shared or dedicated nodes, whereas bare metal machines are always set up as dedicated nodes.

[VPC clusters](/docs/containers?topic=containers-getting-started) are created in your own Virtual Private Cloud that gives you the security of a private cloud environment with the dynamic scalability of a public cloud. You use network access control lists to protect the subnets that your worker nodes are connected to. Worker nodes on VPC clusters are created as virtual machines using either shared infrastructure or dedicated hosts.

For more information, see [Overview of Classic and VPC infrastructure providers](/docs/containers?topic=containers-infrastructure_providers). 


**Where can I learn more about the service?**

Review the following links to find out more about the benefits and responsibilities when you use {{site.data.keyword.openshiftlong_notm}}.

- [Benefits of using {{site.data.keyword.openshiftlong_notm}}](/docs/containers?topic=containers-cs_ov)
- [{{site.data.keyword.openshiftlong_notm}} service architecture](/docs/openshift?topic=openshift-service-architecture)
- [Use cases](/docs/containers?topic=containers-cs_uc_intro)
- [Your responsibilities by using {{site.data.keyword.openshiftlong_notm}}](/docs/containers?topic=containers-responsibilities_iks)
- [Defining your Kubernetes strategy](/docs/containers?topic=containers-strategy)
- [Limitations](/docs/openshift?topic=openshift-openshift_limitations)



## Docker containers
{: #docker_containers}

Built on existing Linux container technology (LXC), the open source project that is named Docker defined templates for how to package software into standardized units, called containers, that include all the elements that an app needs to run. {{site.data.keyword.openshiftlong_notm}} uses `cri-o` as the container runtime to deploy containers from Docker container images into your cluster.
{: shortdesc}

### Key concepts
{: #docker-concepts}

Learn more about the key concepts of Docker.
{: shortdesc}

Image
: A container image is the base for every container that you want to run. Container images are built from a Dockerfile, a text file that defines how to build the image and which build artifacts to include in it, such as the app, the app's configuration, and its dependencies. Images are always built from other images, making them quick to configure. Let someone else do the bulk of the work on an image and then tweak it for your use.

Registry
: An image registry is a place to store, retrieve, and share container images. Images that are stored in a registry can either be publicly available (public registry) or accessible by a small group of users (private registry). {{site.data.keyword.openshiftlong_notm}} offers public images, such as `ibmliberty`, that you can use to create your first containerized app. When it comes to enterprise applications, use a private registry like the one that is provided in {{site.data.keyword.cloud_notm}} to protect your images from being used by unauthorized users.

Container
: Every container is created from an image. A container is a packaged app with all its dependencies so that the app can be moved between environments and run without changes. Unlike virtual machines, containers don't virtualize a device, its operating system, and the underlying hardware. Only the app code, run time, system tools, libraries, and settings are packaged inside the container. Containers run as isolated processes on Ubuntu compute hosts and share the host operating system and its hardware resources. This approach makes a container more lightweight, portable, and efficient than a virtual machine.

### Benefits
{: #docker-benefits}

Review the key benefits of using containers to run your workloads in the cloud.
{: shortdesc}

Containers are agile
: Containers simplify system administration by providing standardized environments for development and production deployments. The lightweight run time enables rapid scale-up and scale-down of deployments. Remove the complexity of managing different operating system platforms and their underlying infrastructures by using containers to help you deploy and run any app on any infrastructure quickly and reliably.

Containers are small
: You can fit many containers in the amount of space that a single virtual machine requires.

Containers are portable
: When you use containers, you can,
  - Reuse pieces of images to build containers.
  - Move app code quickly from staging to production environments.
  - Automate your processes with continuous delivery tools.

Ready to gain deeper knowledge of Docker? [Learn how Docker and {{site.data.keyword.openshiftlong_notm}} work together by completing this course.](https://cognitiveclass.ai/courses/docker-essentials){: external}


## Kubernetes clusters
{: #kubernetes_basics}

![Kubernetes certification badge](images/certified-kubernetes-resized.png "Deployment setup"){: caption="Figure 1. This badge indicates Kubernetes certification for IBM Cloud Container Service." caption-side="bottom"}

The open source project that is named Kubernetes combines running a containerized infrastructure with production workloads, open source contributions, and Docker container management tools. The Kubernetes infrastructure provides an isolated and secure app platform for managing containers that is portable, extensible, and self-healing in case of failovers. For more information, see [What is Kubernetes?](https://www.ibm.com/topics/kubernetes){: external}.
{: shortdesc}


### Key concepts
{: #kubernetes-concepts}

Learn more about the key concepts of Kubernetes as illustrated in the following image.
{: shortdesc}

![Deployment setup of key concepts](images/cs_app_tutorial_mz-components1.png "Deployment setup"){: caption="Figure 2. A description of key concepts for Kubernetes" caption-side="bottom"}

Account
: Your account refers to your {{site.data.keyword.cloud_notm}} account.

Cluster, worker pool, and worker node
: A Kubernetes cluster consists of a master and one or more compute hosts that are called worker nodes. Worker nodes are organized into worker pools of the same flavor, or profile of CPU, memory, operating system, attached disks, and other properties. The worker nodes correspond to the Kubernetes `Node` resource, and are managed by a Kubernetes master that centrally controls and monitors all Kubernetes resources in the cluster. So when you deploy the resources for a containerized app, the Kubernetes master decides which worker node to deploy those resources on, accounting for the deployment requirements and available capacity in the cluster. Kubernetes resources include services, deployments, and pods. For more information, see [Service architecture](/docs/containers?topic=containers-service-arch).

Namespace
: Kubernetes namespaces are a way to divide your cluster resources into separate areas that you can deploy apps and restrict access to, such as if you want to share the cluster with multiple teams. For example, system resources that are configured for you are kept in separate namespaces like `kube-system` or `ibm-system`. If you don't designate a namespace when you create a Kubernetes resource, the resource is automatically created in the `default` namespace. For more information, see the [Kubernetes documentation](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/){: external}.

Service
: A service is a Kubernetes resource that groups a set of pods and provides network connectivity to these pods without exposing the actual private IP address of each pod. You can use a service to make your app available within your cluster or to the public internet. For more information, see the [Kubernetes documentation](https://kubernetes.io/docs/concepts/services-networking/service/){: external}.

Deployment
: A deployment is a Kubernetes resource where you might specify information about other resources or capabilities that are required to run your app, such as services, persistent storage, or annotations. You document a deployment in a configuration YAML file, and then apply it to the cluster. The Kubernetes master configures the resources and deploys containers into pods on the worker nodes with available capacity.

  Define update strategies for your app, including the number of pods that you want to add during a rolling update and the number of pods that can be unavailable at a time. When you perform a rolling update, the deployment checks whether the update is working and stops the rollout when failures are detected.

  A deployment is just one type of workload controller that you can use to manage pods. For help choosing among your options, see [What type of Kubernetes objects can I make for my app?](/docs/openshift?topic=openshift-plan_deploy#object). For more information about deployments, see the [Kubernetes documentation](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/){: external}.
  
Pod
: Every containerized app that is deployed into a cluster is deployed, run, and managed by a Kubernetes resource called a pod. Pods represent small deployable units in a Kubernetes cluster and are used to group the containers that must be treated as a single unit. Usually, each container is deployed in its own pod. However, an app might require a container and other helper containers to be deployed into one pod so that those containers can be addressed by using the same private IP address. For more information, see the [Kubernetes documentation](https://kubernetes.io/docs/concepts/workloads/pods/){: external}.

App
: An app might refer to a complete app or a component of an app. You might deploy components of an app in separate pods or separate worker nodes. For more information, see [Planning app deployments](/docs/containers?topic=containers-plan_deploy) and [Developing Kubernetes-native apps](/docs/containers?topic=containers-app).

### Related resources
{: #kubernetes-resources}

Review how you can learn about Kubernetes concepts and the terminology.
{: shortdesc}

* Familiarize yourself with the product by completing the [Creating clusters tutorial](/docs/openshift?topic=openshift-openshift_tutorial).
* Learn how Kubernetes and {{site.data.keyword.openshiftlong_notm}} work together by completing this [course](https://cognitiveclass.ai/courses/kubernetes-course){: external}.



