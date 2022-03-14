---

copyright: 
  years: 2014, 2022
lastupdated: "2022-03-14"

keywords: openshift

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Benefits and service offerings
{: #cs_ov}



[{{site.data.keyword.openshiftlong}}](https://www.ibm.com/cloud/openshift){: external} is an {{site.data.keyword.cloud_notm}} service, where IBM sets up and helps you manage a cluster of worker nodes that come installed with the OpenShift Container Platform container orchestration software.
{: shortdesc}




## Benefits of using the service
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
:  Choose between [{{site.data.keyword.cloud_notm}} Classic or VPC infrastructure providers](/docs/containers?topic=containers-infrastructure_providers).
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
:   Spread your masters across zones in a [multizone cluster](/docs/openshift?topic=openshift-ha_clusters#multizone) to protect your cluster from zonal failures.

Image security compliance with Vulnerability Advisor
:   Set up your own repo in our secured Docker private image registry where images are stored and shared by all users in the organization.
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





## Comparison between {{site.data.keyword.redhat_openshift_notm}} and community Kubernetes clusters
{: #openshift_kubernetes}

Both {{site.data.keyword.openshiftlong_notm}} and {{site.data.keyword.containerlong_notm}} clusters are production-ready container platforms that are tailored for enterprise workloads. The following table compares and contrasts some common characteristics that can help you choose which container platform is right for your use case.
{: shortdesc}

|Characteristics|Community Kubernetes clusters|{{site.data.keyword.redhat_openshift_notm}} clusters|
|---------------|-------------|-----------------|
|Complete cluster management experience through the {{site.data.keyword.containerlong_notm}} automation tools (API, CLI, console)|Yes|Yes|
|Worldwide availability in single and multizones|Yes|Yes|
|Consistent container orchestration across hybrid cloud providers|Yes|Yes|
|Access to {{site.data.keyword.cloud_notm}} services such as AI|Yes|Yes|
|Software-defined storage Portworx solution available for multizone data use cases|Yes|Yes|
|Create a cluster in an IBM Virtual Private Cloud (VPC)|Yes|Yes|
|Ability to create free clusters|Yes| |
|Latest community Kubernetes distribution|Yes| |
|Scope {{site.data.keyword.cloud_notm}} IAM access policies to access groups for service access roles that sync to cluster RBAC |Yes| |
|Classic infrastructure cluster on only the private network|Yes| |
| GPU bare metal worker nodes | Yes | Yes |
|Integrated IBM Cloud Paks and middleware| |Yes|
|Built-in container image streams, builds, and tooling ([read more](https://cloudowski.com/articles/why-managing-container-images-on-openshift-is-better-than-on-kubernetes/){: external})| |Yes|
|Integrated CI/CD with Jenkins| |Yes|
|Stricter app security context set up by default| |Yes|
|Simplified Kubernetes developer experience, with an app console that is suited for beginners| |Yes|
|Supported operating system| Ubuntu 18.04 x86_64, 16.04 x86_64 (deprecated) |Red Hat Enterprise Linux 7|
|Preferred external traffic networking| Ingress | Router |
|Secured routes encrypted with {{site.data.keyword.hscrypto}} | | Yes |
{: caption="Characteristics of community Kubernetes and {{site.data.keyword.redhat_openshift_notm}} clusters" caption-side="top"}



## Comparison between clusters that run in {{site.data.keyword.cloud_notm}} and standard OCP
{: #compare_ocp}

Because {{site.data.keyword.openshiftlong_notm}} is a managed service, many of the {{site.data.keyword.openshiftlong}} components and global settings that you manually set up in OpenShift Container Platform are set up for you by default in {{site.data.keyword.openshiftlong_notm}}. Review the following differences between {{site.data.keyword.openshiftlong_notm}} clusters and a standard installation of OpenShift Container Platform on your own infrastructure. You can also review the [service architecture](/docs/openshift?topic=openshift-service-architecture) for an overview of how {{site.data.keyword.redhat_openshift_notm}} components are set up in the cluster master and worker nodes, or the [global settings](/docs/openshift?topic=openshift-service-settings#global-settings) that you can or can't configure.
{: shortdesc}

![Version 4 icon.](images/icon-version-43.png) The following comparison applies to clusters that run {{site.data.keyword.redhat_openshift_notm}} version 4. For version 3.11 clusters, the general principles are similar, such as that IBM provides a managed master, but the implementation details differ due to the changes in the underlying OCP version. For more information, see [Comparison between {{site.data.keyword.redhat_openshift_notm}} 3.11 and 4 clusters](#3.11_vs_4.3).
{: note}

|Characteristics|Standard OCP|{{site.data.keyword.openshiftlong_notm}}|
|---------------|----------------------|----------------------------------------|
| Cluster master (control plane) | You set up control plane components like the API server and etcd on machines that get the `master` role. You can modify the control plane components, but keep in mind that you are responsible for backing up, restoring, and making control plane data highly available. | IBM sets up the master, manages the control plane components, and automatically applies master patch updates for you. The masters are highly available and backed up automatically.|
| Compute machines (worker nodes) | You create your own compatible compute machines, set up compatible network connectivity, SSH into the machines, install OCP, and register the machines as worker nodes in the cluster. Your machines might be installer-provisioned infrastructure (IPI) for a guided setup, or user-provisioned infrastructure (UPI) for more control and subsequent administration on your end. You are responsible for maintaining and updating the worker nodes. You can install updates from the {{site.data.keyword.redhat_openshift_notm}} web console. | You select the flavor of worker nodes that you want to add to your cluster, and IBM automatically connects the worker nodes to the cluster and installs OCP. In this sense, the installation is similar to IPI for you because you don't have to manage all the infrastructure and network settings. IBM also provides patch updates that you can choose to apply to your worker nodes, from the {{site.data.keyword.cloud_notm}} interface (not the {{site.data.keyword.redhat_openshift_notm}} web console). SSH is disabled for added security. |
| OCP versions and patch updates | You are responsible for updating the underlying infrastructure for the master and worker nodes. You can use the {{site.data.keyword.redhat_openshift_notm}} web console to update OCP versions. | IBM automatically applies updates to the master, and provides version updates and security patch updates for the worker nodes. You choose when to apply these updates to your worker nodes, from the {{site.data.keyword.cloud_notm}} interface (not the {{site.data.keyword.redhat_openshift_notm}} web console). Supported versions might vary from standard OpenShift Container Platform.|
| Autoscaling compute machines | You can set up a `ClusterAutoscaler` resource. | You can set up the [cluster autoscaler plug-in](/docs/openshift?topic=openshift-cluster-scaling-classic-vpc). |
| Worker node operating system | CoreOS or RHEL. | RHEL 7. |
| Support | Provided per the terms of your Red Hat subscription or cloud provider. You can use the `oc adm must-gather` tool to help gather information. | Provided by [{{site.data.keyword.cloud_notm}} Support](https://www.ibm.com/cloud/support){: external}. You can use the `oc adm must-gather` tool, or the [Diagnostics and Debug Tool](/docs/openshift?topic=openshift-debug-tool) to help gather information. |
| {{site.data.keyword.redhat_openshift_notm}} web console | You set up and can configure or disable the {{site.data.keyword.redhat_openshift_notm}} web console. | The {{site.data.keyword.redhat_openshift_notm}} web console is set up for you. You can't configure or disable the web console. IBM also provides the [{{site.data.keyword.redhat_openshift_notm}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external} to manage your cluster infrastructure. |
| Authentication | An OAuth server is provided, but you configure the token settings and identity provider to control access to the cluster. You also manage RBAC to control user access within the cluster. | IBM automatically sets up the OAuth server to use {{site.data.keyword.cloud_notm}} IAM. You can't change the identity provider. {{site.data.keyword.cloud_notm}} IAM is also set up to [automatically sync to RBAC](/docs/openshift?topic=openshift-access_reference#service) so that you can use IAM to manage access to and within the cluster. |
| Container network for clusters | The cluster network operator sets up the SDN container network interface (CNI) plug-in. You can change the CNI plug-in, configure multiple networks, or attach a hardware network such as single root I/O virtualization (SR-IOV). | Calico is set up for you. You can't change the CNI plug-in, configure multiple networks, or attach a hardware network.|
| Ingress | You can use the Ingress operator to set up one or more HAProxy-based Ingress controllers. You can route traffic to your apps by specifying `Route` or `Ingress` resources. | When you create a cluster, a default Ingress subdomain is set up for you. One HAProxy-based router is set up for each Ingress controller, and one router service is automatically created in each zone that you have worker nodes in. You can route traffic to your apps by specifying `Route` or `Ingress` resources. For more information, see [About Ingress in {{site.data.keyword.redhat_openshift_notm}} version 4](/docs/openshift?topic=openshift-ingress-about-roks4). |
| Storage | You must set up persistent volumes to be backed up by a storage provider. OpenShift Data Foundation is available. | IBM automatically sets up storage providers such as {{site.data.keyword.cloud_notm}} File and Block. OpenShift Data Foundation is not available. For supported storage options, see [Planning highly available persistent storage](/docs/openshift?topic=openshift-storage_planning). |
| Image registry | The cluster is set up with an internal registry to pull images. If your cluster has public network access, you can pull images automatically from Docker Hub. To pull images from other registries, you must set up image pull secrets. You set up the internal registry to back up images to a cloud storage provider. Stored images are not available across clusters. | The internal registry is set up to back up images automatically to a bucket in your {{site.data.keyword.cos_full_notm}} instance. Your cluster has image pull secrets automatically set up to pull images from default registries, including {{site.data.keyword.registrylong_notm}}. You can also set up the internal registry to work with {{site.data.keyword.registrylong_notm}}, which your cluster is also automatically set up to pull images from. For more information, see [Setting up an image registry](/docs/openshift?topic=openshift-registry). |
| Operators and OperatorHub | OpenShift Container Platform sets up many operators to manage default components for the cluster. You can also use the OperatorHub to install other operators such as from 3rd-party providers. | IBM sets up many of the same operators as OCP to manage default component for the cluster. However, because IBM manages the master and provides you with {{site.data.keyword.cloud_notm}} APIs to manage your cloud infrastructure, some operators, such as the machine set operator and other components as noted in this table, are not set up or configurable. You can also use the OperatorHub to [install other operators](/docs/openshift?topic=openshift-operators) such as from 3rd-party providers. Note that operators that you install or create are not supported by IBM, and might come with their own support terms and pricing.|
| Projects, builds, and apps | OpenShift Container Platform provides tools such as projects, build configs, and the internal registry that you can use to deploy your apps while following a cloud-native, continuous integration and continuous delivery (CI/CD) methodology. | {{site.data.keyword.openshiftlong_notm}} clusters come with all the same configurable project and build components as OCP clusters. You can also choose to integrate your cluster with {{site.data.keyword.cloud_notm}} services like [{{site.data.keyword.contdelivery_short}}](/docs/openshift?topic=openshift-cicd). |
| Cluster health | You can also set up logging, monitoring, and metering tools by installing and configuring various operators. These solutions are cluster-specific and not highly available unless you back them up. | Your clusters feature one-click integrations with {{site.data.keyword.la_full_notm}} and {{site.data.keyword.mon_full_notm}} for enterprise-grade, persistent monitoring and logging solutions across clusters. You can also install the logging and monitoring operators as with standard OCP, but you might have to adjust the configuration settings. For more information, see [Logging and monitoring cluster health](/docs/openshift?topic=openshift-health). |
| Migrating clusters | You can use the cluster migrator operator to migrate clusters from one major version to another. Migration requires separate clusters; you can't update a cluster from one major version to another. Various open source tools might be used, but are not officially supported. | As with standard OpenShift Container Platform, you can't update a cluster from one major version to another. If you use a third-party open source tool such as the [cluster migrator operator](https://github.com/konveyor/mig-operator){: external}, the tool is not supported by IBM and might have limitations such as the migration UI being unavailable. |
| Container-native virtualization | You can set up [container-native virtualization add-on](https://docs.openshift.com/container-platform/4.8/virt/about-virt.html){: external} on bare metal machines, but not on virtual machines.<p class="note">Container-native virtualization is not supported by IBM. If you experience issues, you are responsible for resolving the issues and any impact to your workloads.</p>|
| Serverless workloads | You can set up [{{site.data.keyword.redhat_openshift_notm}} Serverless](https://cloud.redhat.com/learn/topics/serverless){: external}. | You can also set up {{site.data.keyword.redhat_openshift_notm}} Serverless. |
| Service mesh | You can set up the [Red Hat {{site.data.keyword.redhat_openshift_notm}} Service Mesh](https://docs.openshift.com/container-platform/4.8/service_mesh/v1x/installing-ossm.html){: external}. | You can also set up the Red Hat {{site.data.keyword.redhat_openshift_notm}} Service Mesh, but you must [apply a network policy](https://gist.githubusercontent.com/kitch/39c504a2ed9e381c2aadea436d5b52e4/raw/d8efa69f41d41425b16bb363a881a98d40d3708c/mesh-policy.yaml){: external} for the service mesh ingress to work.|
| API and CLI tools | OpenShift Container Platform clusters are set up with access to Kubernetes and {{site.data.keyword.redhat_openshift_notm}} API resources. You can also install command line tools such as `oc` and `odo`. | {{site.data.keyword.openshiftlong_notm}} clusters come with the same capabilities to use the Kubernetes and {{site.data.keyword.redhat_openshift_notm}} API and CLI tools. Additionally, you can use the {{site.data.keyword.cloud_notm}} [API](/docs/openshift?topic=openshift-cs_api_install) and [CLI](/docs/openshift?topic=openshift-openshift-cli) tools to manage your cluster infrastructure and integrate other cloud services with your cluster.|
{: caption="Comparison between clusters that run in {{site.data.keyword.cloud_notm}} and standard OCP" caption-side="top"}
{: summary="The rows are read from left to right. In the first column is the characteristic that differs between standard OpenShift Container Platform installations in the second column and {{site.data.keyword.openshiftlong_notm}} clusters in the third column."}




## Comparison between {{site.data.keyword.redhat_openshift_notm}} 3.11 and 4 clusters
{: #3.11_vs_4.3}

Review the following characteristics to decide which {{site.data.keyword.openshiftlong_notm}} cluster version to create. In both {{site.data.keyword.openshiftlong_notm}} versions, you get the same overall [benefits](#benefits), such as the IBM-managed master, version and security patch updates, and IBM Support according to your [terms of service](/docs/overview/terms-of-use?topic=overview-terms#terms).
{: shortdesc}

![Version 3.11 icon.](images/icon-version-311.png) {{site.data.keyword.redhat_openshift_notm}} version 3.11 is deprecated, and becomes unsupported on 6 June 2022 (date subject to change).
{: deprecated}

You can't update from an {{site.data.keyword.redhat_openshift_notm}} 3.11 to 4 cluster. Instead, [create a version 4 cluster](/docs/openshift?topic=openshift-clusters).
{: note}

|Characteristics|{{site.data.keyword.redhat_openshift_notm}} 3.11|{{site.data.keyword.redhat_openshift_notm}} 4|
|---------------|-------------|-----------------|
| Supported version? | Deprecated | Supported |
| RHEL version | 7 | 7 |
| Kubernetes version | 1.11 | 1.16 |
| CRI-O runtime version | 1.11 | 1.16 |
| Worker node DNS | `dnsmasq` daemon set | `openshift-dns` operator (CoreDNS) |
| App service integration tool | Service catalog | Operators |
| Virtual private cloud (VPC) support | | Yes |
| Managed {{site.data.keyword.redhat_openshift_notm}} master | Yes | Yes |
| Provided version and security patch updates | Yes | Yes |
| Encryption with {{site.data.keyword.keymanagementservicelong_notm}} | Yes | |
| Istio | | [Service mesh operator](https://docs.openshift.com/container-platform/4.8/service_mesh/v1x/servicemesh-release-notes.html){: external} |
| Debug tool | Yes | Yes |
| Cluster autoscaler | Yes | Yes |
| Classic File Storage | Yes | Yes |
| Classic Block Storage | Yes | Yes |
| {{site.data.keyword.cos_full_notm}} | Yes | Yes |
| Portworx | Yes | Yes |
| Subdomains for ingress | Separate subdomains for `Ingress` and `Route` resources | Same subdomain for both `Ingress` and `Router` resources |
| Ingress resources with {{site.data.keyword.openshiftlong_notm}} ALBs | Yes | |
| Ingress resources with {{site.data.keyword.redhat_openshift_notm}} Ingress controllers | | Yes |
{: caption="Supported features in {{site.data.keyword.redhat_openshift_notm}} 3.11 and 4 clusters" caption-side="top"}






