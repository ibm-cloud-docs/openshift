---

copyright:
  years: 2014, 2020
lastupdated: "2020-04-01"

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


# Benefits and service offerings
{: #cs_ov}


{{site.data.keyword.openshiftlong}} is an {{site.data.keyword.cloud_notm}} service, where IBM sets up and helps you manage a cluster of worker nodes that come installed with the OpenShift Container Platform container orchestration software.
{: shortdesc}

Check out the following [videos and product tours](https://www.ibm.com/demos/collection/Red-Hat-OpenShift-on-IBM-Cloud/?lc=null){: external} to learn more about Red Hat OpenShift on IBM Cloud.


## Benefits of using the service
{: #benefits}

With Red Hat OpenShift on IBM Cloud, your developers have a fast and secure way to containerize and deploy enterprise workloads in Kubernetes clusters. OpenShift clusters build on Kubernetes container orchestration that offers consistency and flexibility for your development lifecycle operations.

Your OpenShift workloads can scale across IBM’s global footprint of data centers and multizone regions. At the same time, you’re able to uniformly monitor, log, and secure apps. Because IBM manages the service, you can focus on innovating with high-value {{site.data.keyword.cloud_notm}} services and middleware, such as AI and analytics. You also have access to Red Hat packaged open-source tools, including your favorite app runtimes, frameworks, databases, and more.

Ready to get started? Try out the [creating a Red Hat OpenShift on IBM Cloud cluster tutorial](/docs/openshift?topic=openshift-openshift_tutorial).

|Benefit|Description|
|-------|-----------|
|Choice of container platform provider | <ul><li>Deploy clusters with **OpenShift** or community **Kubernetes** installed as the container platform orchestrator.</li><li>Choose the developer experience that fits your company, or run workloads across both OpenShift or community Kubernetes clusters.</li><li>Built-in integrations from the {{site.data.keyword.cloud_notm}} console to the Kubernetes dashboard or OpenShift web console.</li><li>Single view and management experience of all your OpenShift or community Kubernetes clusters from {{site.data.keyword.cloud_notm}}.</li><li>For more information, see [Comparison between OpenShift and community Kubernetes clusters](#openshift_kubernetes).</li></ul>|
|Single-tenant Kubernetes clusters with compute, network, and storage infrastructure isolation|<ul><li>Create your own customized infrastructure that meets the requirements of your organization.</li><li>Provision a dedicated and secured OpenShift master, worker nodes, virtual networks, and storage by using the resources provided by IBM Cloud infrastructure.</li><li>Fully managed Kubernetes master that is continuously monitored and updated by {{site.data.keyword.IBM_notm}} to keep your cluster available.</li><li>Option to provision worker nodes as bare metal servers for compute-intensive workloads such as data and AI.</li><li>Store persistent data, share data between Kubernetes pods, and restore data when needed with the integrated and secure volume service.</li><li>Benefit from full support for all native Kubernetes APIs.</li></ul>|
| Multizone clusters to increase high availability | <ul><li>Easily manage worker nodes of the same flavor (CPU, memory, virtual or physical) with worker pools.</li><li>Guard against zone failure by spreading nodes evenly across select multizones and by using anti-affinity pod deployments for your apps.</li><li>Decrease your costs by using multizone clusters instead of duplicating the resources in a separate cluster.</li><li>Benefit from automatic load balancing across apps with the multizone load balancer (MZLB) that is set up automatically for you in each zone of the cluster.</li></ul>|
| Highly available masters | <ul><li>Reduce cluster downtime such as during master updates with highly available masters that are provisioned automatically when you create a cluster.</li><li>Spread your masters across zones in a [multizone cluster](/docs/openshift?topic=openshift-ha_clusters#multizone) to protect your cluster from zonal failures.</li></ul> |
|Image security compliance with Vulnerability Advisor|<ul><li>Set up your own repo in our secured Docker private image registry where images are stored and shared by all users in the organization.</li><li>Benefit from automatic scanning of images in your private {{site.data.keyword.cloud_notm}} registry.</li><li>Review recommendations specific to the operating system used in the image to fix potential vulnerabilities.</li></ul>|
|Continuous monitoring of the cluster health|<ul><li>Use the cluster dashboard to quickly see and manage the health of your cluster, worker nodes, and container deployments.</li><li>Find detailed consumption metrics by using {{site.data.keyword.mon_full}} and quickly expand your cluster to meet work loads.</li><li>Review logging information by using {{site.data.keyword.la_full}} to see detailed cluster activities.</li></ul>|
|Secure exposure of apps to the public|<ul><li>Choose between a public IP address, an {{site.data.keyword.IBM_notm}} provided route, or your own custom domain to access services in your cluster from the internet.</li></ul>|
|{{site.data.keyword.cloud_notm}} service integration|<ul><li>Add extra capabilities to your app through the integration of {{site.data.keyword.cloud_notm}} services, such as Watson APIs, Blockchain, data services, or Internet of Things.</li></ul>|
{: caption="Benefits of the {{site.data.keyword.containerlong_notm}}" caption-side="top"}

<br />



## Comparison between OpenShift and community Kubernetes clusters
{: #openshift_kubernetes}

Both OpenShift and community Kubernetes clusters are production-ready container platforms that are tailored for enterprise workloads. The following table compares and contrasts some common characteristics that can help you choose which container platform is right for your use case.
{: shortdesc}

|Characteristics|Community Kubernetes clusters|OpenShift clusters|
|---------------|-------------|-----------------|
|Complete cluster management experience through the {{site.data.keyword.containerlong_notm}} automation tools (API, CLI, console)|<img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" />|<img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" />|
|Worldwide availability in single and multizones|<img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" />|<img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" />|
|Consistent container orchestration across hybrid cloud providers|<img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" />|<img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" />|
|Access to {{site.data.keyword.cloud_notm}} services such as AI|<img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" />|<img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" />|
|Software-defined storage Portworx solution available for multizone data use cases|<img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" />|<img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" />|
|Create a cluster in an IBM Virtual Private Cloud (VPC)|<img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" />||
|Ability to create free clusters|<img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" />| |
|Latest community Kubernetes distribution|<img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" />| |
|Cluster on only the private network|<img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" />| |
|Integrated IBM Cloud Paks and middleware| |<img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" />|
|Built-in container image streams, builds, and tooling ([read more](https://cloudowski.com/articles/why-managing-container-images-on-openshift-is-better-than-on-kubernetes/){: external})| |<img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" />|
|Integrated CI/CD with Jenkins| |<img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" />|
|Stricter app security context set up by default| |<img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" />|
|Simplified Kubernetes developer experience, with an app console that is suited for beginners| |<img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" />|
|Supported operating system| Ubuntu 16.64, 18.64 |Red Hat Enterprise Linux 7|
|Preferred external traffic networking| Ingress | Router |
{: caption="Characteristics of community Kubernetes and OpenShift clusters" caption-side="top"}


## Comparison between OpenShift 3.11 and 4.3 clusters
{: #3.11_vs_4.3}

Review the following characteristics to decide which Red Hat OpenShift on IBM Cloud cluster version to create. In both Red Hat OpenShift on IBM Cloud versions, you get the same overall [benefits](#benefits), such as the IBM-managed master, version and security patch updates, and IBM Support according to your [terms of service](/docs/overview/terms-of-use?topic=overview-terms#terms).
{: shortdesc}

You cannot update from an OpenShift 3.11 to 4.3 cluster. Instead, [create a 4.3 cluster](/docs/openshift?topic=openshift-clusters).
{: note}

|Characteristics|OpenShift 3.11|OpenShift 4.3|
|---------------|-------------|-----------------|
| RHEL version | 7 | 7 |
| Kubernetes version | 1.11 | 1.16 |
| CRI-O runtime version | 1.11 | 1.16 |
| Worker node DNS | `dnsmasq` daemon set | `openshift-dns` operator (CoreDNS) |
| App service integration tool | Service catalog | Operators |
| Managed OpenShift master | <img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" /> | <img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" /> |
| Provided version and security patch updates | <img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" /> | <img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" /> |
| Encryption with {{site.data.keyword.keymanagementservicelong_notm}} | <img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" /> | |
| Istio | | [Service mesh operator](https://docs.openshift.com/container-platform/4.3/service_mesh/servicemesh-release-notes.html){: external} |
| Knative | | [Serverless operator](https://docs.openshift.com/container-platform/4.3/serverless/serverless-getting-started.html){: external}|
| Debug tool | <img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" /> | <img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" /> |
| Cluster autoscaler | <img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" /> | <img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" /> |
| Classic File Storage | <img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" /> | <img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" /> |
| Classic Block Storage | <img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" /> | <img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" /> |
| {{site.data.keyword.cos_full_notm}} | <img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" /> | <img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" /> |
| Portworx | <img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" /> | |
| Subdomains for ingress | Separate subdomains for `Ingress` and `Route` resources | Same subdomain for both `Ingress` and `Router` resources |
| Ingress resources with Red Hat OpenShift on IBM Cloud ALBs | <img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" /> | |
| Ingress resources with OpenShift Ingress controllers | | <img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" /> |
{: caption="Supported features in OpenShift 3.11 and 4.3 clusters" caption-side="top"}





