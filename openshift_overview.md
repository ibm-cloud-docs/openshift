---

copyright:
  years: 2014, 2020
lastupdated: "2020-06-08"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift

---

{:codeblock: .codeblock}
{:deprecated: .deprecated}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:gif: data-image-type='gif'}
{:help: data-hd-content-type='help'}
{:important: .important}
{:new_window: target="_blank"}
{:note: .note}
{:pre: .pre}
{:preview: .preview}
{:screen: .screen}
{:shortdesc: .shortdesc}
{:support: data-reuse='support'}
{:table: .aria-labeledby="caption"}
{:tip: .tip}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}


# Overview
{: #overview}

Learn more about [{{site.data.keyword.openshiftlong}}](https://www.ibm.com/cloud/openshift){: external}, its capabilities, and the options that are available to you to customize the cluster to your needs.
{: shortdesc}

## Understanding Red Hat OpenShift on IBM Cloud
{: #service-concepts}

Review frequently asked questions and key technologies that Red Hat OpenShift on IBM Cloud uses.
{: shortdesc}

**What is Red Hat OpenShift on IBM Cloud and how does it work?** </br>
Red Hat OpenShift on IBM Cloud is a managed offering to create your own OpenShift cluster of compute hosts to deploy and manage containerized apps on {{site.data.keyword.cloud_notm}}. Red Hat OpenShift on IBM Cloud provides intelligent scheduling, self-healing, horizontal scaling, service discovery and load balancing, automated rollouts and rollbacks, and secret and configuration management for your apps. Combined with an intuitive user experience, built-in security and isolation, and advanced tools to secure, manage, and monitor your cluster workloads, you can rapidly deliver highly available and secure containerized apps in the public cloud.

**What is Kubernetes?** </br>
Kubernetes is an open source platform for managing containerized workloads and services across multiple hosts, and offers management tools for deploying, automating, monitoring, and scaling containerized apps with minimal to no manual intervention. For an overview of key Kubernetes concepts, see [Kubernetes clusters](#kubernetes_basics). To dive deeper into Kubernetes, see the [Kubernetes documentation](https://kubernetes.io/docs/home/?path=users&persona=app-developer&level=foundational).

**What are containers?** </br>
Containers provide a standard way to package your application's code, configurations, and dependencies into a single unit that can run as a resource-isolated process on a compute server. To run your app in Kubernetes on Red Hat OpenShift on IBM Cloud, you must first containerize your app by creating a container image that you store in a container registry. For an overview of key Docker concepts and benefits, see [Docker containers](#docker_containers). To dive deeper into Docker, see the [Docker documentation](https://docs.docker.com/).

**What is OpenShift?**<br>
OpenShift is a Kubernetes container platform that provides a trusted environment to run enterprise workloads. It extends the Kubernetes platform with built-in software to enhance app lifecycle development, operations, and security. With OpenShift, you can consistently deploy your workloads across hybrid cloud providers and environments. For more information about the differences between the community Kubernetes and OpenShift cluster offerings, see the [comparison table](/docs/openshift?topic=openshift-cs_ov#openshift_kubernetes).

**What compute host infrastructure does the service offer?** </br>
With Red Hat OpenShift on IBM Cloud, you can create your cluster of compute hosts on classic {{site.data.keyword.cloud_notm}} infrastructure.

[Classic clusters](/docs/containers?topic=containers-getting-started) are created on your choice of virtual or bare metal worker nodes that are connected to VLANs. If you require additional local disks, you can also choose one of the bare metal flavors that are designed for software-defined storage solutions, such as Portworx. Depending on the level of hardware isolation that you need, virtual worker nodes can be set up as shared or dedicated nodes, whereas bare metal machines are always set up as dedicated nodes.

**Where can I learn more about the service?** </br>
Review the following links to find out more about the benefits and responsibilities when you use Red Hat OpenShift on IBM Cloud.

- [Benefits of using Red Hat OpenShift on IBM Cloud](/docs/openshift?topic=openshift-cs_ov)
- [Red Hat OpenShift on IBM Cloud service architecture](/docs/openshift?topic=openshift-service-arch#service-architecture)
- [Use cases](/docs/containers?topic=containers-cs_uc_intro)
- [Your responsibilities by using Red Hat OpenShift on IBM Cloud](/docs/openshift?topic=openshift-responsibilities_iks)
- [Defining your Kubernetes strategy](/docs/openshift?topic=openshift-strategy)
- [Limitations](/docs/openshift?topic=openshift-openshift_limitations)
- Learn how you can use Red Hat OpenShift on IBM Cloud to modernize and run containerized apps in these <a href="https://www.ibm.com/demos/collection/Containers-(Kubernetes)-on-IBM-Cloud/?lc=null">videos</a>.

<br />



## Docker containers
{: #docker_containers}

Built on existing Linux container technology (LXC), the open source project that is named Docker defined templates for how to package software into standardized units, called containers, that include all of the elements that an app needs to run. Red Hat OpenShift on IBM Cloud uses `cri-o` as the container runtime to deploy containers from Docker container images into your cluster.
{:shortdesc}

### Key concepts
{: #docker-concepts}

Learn more about the key concepts of Docker.
{: shortdesc}

<dl>
<dt>Image</dt>
<dd>A container image is the base for every container that you want to run. Container images are built from a Dockerfile, a text file that defines how to build the image and which build artifacts to include in it, such as the app, the app's configuration, and its dependencies. Images are always built from other images, making them quick to configure. Let someone else do the bulk of the work on an image and then tweak it for your use.</dd>
<dt>Registry</dt>
<dd>An image registry is a place to store, retrieve, and share container images. Images that are stored in a registry can either be publicly available (public registry) or accessible by a small group of users (private registry). Red Hat OpenShift on IBM Cloud offers public images, such as `ibmliberty`, that you can use to create your first containerized app. When it comes to enterprise applications, use a private registry like the one that is provided in {{site.data.keyword.cloud_notm}} to protect your images from being used by unauthorized users.
</dd>
<dt>Container</dt>
<dd>Every container is created from an image. A container is a packaged app with all of its dependencies so that the app can be moved between environments and run without changes. Unlike virtual machines, containers do not virtualize a device, its operating system, and the underlying hardware. Only the app code, run time, system tools, libraries, and settings are packaged inside the container. Containers run as isolated processes on Ubuntu compute hosts and share the host operating system and its hardware resources. This approach makes a container more lightweight, portable, and efficient than a virtual machine.</dd>
</dl>

### Benefits
{: #docker-benefits}

Review the key benefits of using containers to run your workloads in the cloud.
{: shortdesc}

<dl>
<dt>Containers are agile</dt>
<dd>Containers simplify system administration by providing standardized environments for development and production deployments. The lightweight run time enables rapid scale-up and scale-down of deployments. Remove the complexity of managing different operating system platforms and their underlying infrastructures by using containers to help you deploy and run any app on any infrastructure quickly and reliably.</dd>
<dt>Containers are small</dt>
<dd>You can fit many containers in the amount of space that a single virtual machine requires.</dd>
<dt>Containers are portable</dt>
<dd><ul>
  <li>Reuse pieces of images to build containers. </li>
  <li>Move app code quickly from staging to production environments.</li>
  <li>Automate your processes with continuous delivery tools.</li></ul>
</dd>
</dl>

Ready to gain deeper knowledge of Docker? [Learn how Docker and Red Hat OpenShift on IBM Cloud work together by completing this course.](https://cognitiveclass.ai/courses/docker-essentials){:external}

<br />


## Kubernetes clusters
{: #kubernetes_basics}

<img src="images/certified-kubernetes-resized.png" style="padding-right: 10px;" align="left" alt="This badge indicates Kubernetes certification for IBM Cloud Container Service."/>The open source project that is named Kubernetes combines running a containerized infrastructure with production workloads, open source contributions, and Docker container management tools. The Kubernetes infrastructure provides an isolated and secure app platform for managing containers that is portable, extensible, and self-healing in case of failovers. For more information, check out the [Kubernetes](https://www.ibm.com/cloud/learn/kubernetes) blog post.
{:shortdesc}

</br>

### Key concepts
{: #kubernetes-concepts}

Learn more about the key concepts of Kubernetes as illustrated in the following image.
{: shortdesc}

![Deployment setup](images/cs_app_tutorial_mz-components1.png)

<dl>
<dt>Account</dt>
<dd>Your account refers to your {{site.data.keyword.cloud_notm}} account.</dd>
<dt>Cluster</dt>
<dd>A Kubernetes cluster consists of one or more compute hosts that are called worker nodes. Worker nodes are managed by a Kubernetes master that centrally controls and monitors all Kubernetes resources in the cluster. So when you deploy the resources for a containerized app, the Kubernetes master decides which worker node to deploy those resources on, accounting for the deployment requirements and available capacity in the cluster. Kubernetes resources include services, deployments, and pods.</dd>
<dt>Service</dt>
<dd>A service is a Kubernetes resource that groups a set of pods and provides network connectivity to these pods without exposing the actual private IP address of each pod. You can use a service to make your app available within your cluster or to the public internet.</dd>
<dt>Deployment</dt>
<dd>A deployment is a Kubernetes resource where you might specify information about other resources or capabilities that are required to run your app, such as services, persistent storage, or annotations. You document a deployment in a configuration YAML file, and then apply it to the cluster. The Kubernetes master configures the resources and deploys containers into pods on the worker nodes with available capacity.</br></br>Define update strategies for your app, including the number of pods that you want to add during a rolling update and the number of pods that can be unavailable at a time. When you perform a rolling update, the deployment checks whether the update is working and stops the rollout when failures are detected.</dd>
<dt>Pod</dt>
<dd>Every containerized app that is deployed into a cluster is deployed, run, and managed by a Kubernetes resource that is called a pod. Pods represent small deployable units in a Kubernetes cluster and are used to group the containers that must be treated as a single unit. In most cases, each container is deployed in its own pod. However, an app might require a container and other helper containers to be deployed into one pod so that those containers can be addressed by using the same private IP address.</dd>
<dt>App</dt>
<dd>An app might refer to a complete app or a component of an app. You might deploy components of an app in separate pods or separate worker nodes.</dd></dl>

### Related resources
{: #kubernetes-resources}

Review how you can learn about Kubernetes concepts and the terminology.
{: shortdesc}

* Familiarize yourself with the product by completing the [Creating clusters tutorial](/docs/openshift?topic=openshift-openshift_tutorial).
* Learn how Kubernetes and Red Hat OpenShift on IBM Cloud work together by completing this [course](https://cognitiveclass.ai/courses/kubernetes-course).



