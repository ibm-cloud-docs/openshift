---

copyright:
  years: 2025, 2026
lastupdated: "2026-02-16"


keywords: openshift, acm, advanced cluster management, manage cluster, management, addon, add-on, acm addon

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}


# About the Advanced Cluster Management add-on (select regions only)
{: #acm-about}


The Advanced Cluster Management (ACM) add-on provides a simplified way to manage, observe, and operate virtual machines (VMs) and clusters from a single control plane. 
{: shortdesc}

The Advanced Cluster Management add-on is available for select regions only.
{: important}

ACM provides the following key capabilities for cluster and VM management.
- Full lifecycle management of Kubernetes clusters and VMs
- Policy-based governance 
- Configuration compliance
- GitOps-enabled application deployment across multiple environments
- operational consistency
- Security enforcement
- Fleet-wide visibility for clusters and VMs
- Disaster recovery


When you install ACM, you choose between two plans that provide additional features and benefits on top of those listed above: **ACM for Virtualization**, which simplifies the management of VMs deployed to Red Hat OpenShift clusters, or **ACM for Kubernetes**, which provides tools to manage clusters and applications, whether containerized or virtualized, from a central console.

## How it works
{: #how}

The ACM add-on is [installed onto a Red Hat OpenShift cluster](/docs/openshift?topic=openshift-acm&interface=ui#install-ui) that acts as the **hub cluster**. During or after installation, you import one or more **managed clusters** that you want to manage with ACM. From the hub cluster, you can access your multi-cluster dashboard to manage, observe and operate the managed clusters that you imported. 

## ACM plan overviews
{: #overviews}

Review the description of each ACM plan.

[Advanced Cluster Management for Virtualization](#virt)
:   - ACM for Virtualization is a centralized tool that simplifies the management of virtual machines (VMs) deployed to Red Hat OpenShift® Virtualization Engine clusters as well as the clusters themselves. This license type provides a centralized platform for provisioning, monitoring and decomissioning VMs across multiple clusters.
:   - This solution is a version of Red Hat Advanced Cluster Management for Kubernetes and is designed for organizations that want to manage VMs exclusively.

For the ACM for Virtualization plan, it is recommended that your managed clusters run bare metal worker nodes.  
{: tip}


[Advanced Cluster Management for Kubernetes](#kube)
:   - ACM for Kubernetes provides the capabilities to address common challenges that administrators and site reliability engineers face when managing multiple clusters. Clusters and applications, whether containerized or virtualized, are all visible and managed from a central console, with preconfigured governance policies that can be applied consistently across environments. Users can run their operations from anywhere on Red Hat OpenShift® and manage other supported Kubernetes clusters in their fleet.


## ACM for Virtualization
{: #virt}

Learn about the features and benefits of the ACM for Virtualization plan.

Centralized console for direct VM management
:   Benefit from increased operational efficiency and reduced context switching. 

Dynamic search
:   Search and see all VMs in a fleet to reduce  complexity. 

Multi-cluster observability including ready-to-use dashboards
:   See the health of VMs and virtualization infrastructure from centrally collected alerts and make optimization plans.

VM-specific actions
:   Manage VMs with intuitive controls to start, stop, restart, pause, resume, and launch by utilizing advanced search capabilities in Red Hat Advanced Cluster Management for Virtualization. 

ApplicationSets for managing VMs applications
:   Deploy VM applications from code repositories to ease deployment and streamline management at scale. 
Control plane decoupled from data plane
:   Reduce costs and improve efficiency by hosting multiple control planes on a single Red Hat OpenShift cluster. 

Pay for what you need
:   Pay only for the capabilities you need. Advanced Cluster Management for Virtualization is a focused subscription that covers VM management capabilities.


## ACM for Kubernetes
{: #kube}

Learn about the features and benefits the ACM for Kubernetes plan.

Fleet management
:   Access a unified fleet management control plane that aids in provisioning clusters and applications and enhances cluster lifecycle management.
:   - Simplified IT operations with self-service cluster setup to reduce operational overhead.
:   - End-to-end visibility and control from a central console to reduce context switching and cognitive load.
:   - Hub-and-spoke architecture for managing all configurations and Kubernetes clusters.
:   - Integration with all major cloud providers and Cloud Native Computing Foundation (CNCF)-conformant Kubernetes distributions for wide operational control.
:   - Enhanced cluster lifecycle management with features like worker pool scaling and cluster hibernation.

Fleet observability
:   Utilize comprehensive multi-cluster observability of fleet health for increased visibility.
:   - Customized dashboards based on defined metrics.
:   - Enhanced SRE experience with included dashboards.
:   - Proactive monitoring of cluster health and performance to help decrease mean time to resolution.
:   - Fleet health monitoring with ability to sort, filter, and scan individual clusters and user workloads.
:   - Dynamic search to identify, isolate, and resolve issues across distributed workloads.
:   - Integration with Red Hat Lightspeed for Red Hat OpenShift to provide intelligent analysis.

Application lifecycle deployment
:   Rapidly and consistently deploy workloads across a fleet or for a single cluster.
:   - GitOps integrations for automatic and consistent application deployments and content delivery.
:   - Increased application availability with placement integration.
:   - Application topology view for wider visibility of application health.
:   - Persistent volume replication for application migration.
:   - Multisite, multicluster disaster recovery capabilities to recover and continue critical applications. 

Multicluster observability for fleet health and optimization
:   Deliver an enhanced site reliability engineering (SRE) experience with out-of-the-box multicluster dashboards that can store long-term historical data and provide an overview of fleet health and optimization. 

Unified multicluster lifecycle management
:   Create, upgrade, and destroy Kubernetes clusters reliably, consistently, and at scale by using an open source programming model that supports Infrastructure as Code (IaC) best practices and design principles. 

Configuration management with policy-based governance
:   Implement automated governance to continuously verify and maintain optimal configuration settings across critical IT domains, including cluster infrastructure, identity and access management, network management, cost optimization, security and compliance. 

Advanced application lifecycle management
:   Use open standards and deploy applications, using placement rules that are integrated into existing continuous integration and continuous delivery (CI/CD) pipelines and governance controls. 

Edge management at scale
:   With single-node OpenShift clusters and Red Hat Advanced Cluster Management, continuously scale while ensuring availability in high-latency, low-bandwidth edge use cases. 

Business continuity
:   Use Red Hat Advanced Cluster Management, along with the broader Red Hat portfolio, to ensure the applications stay up and running. 


## Next steps
{: #next}

Get started using ACM by [installing the add-on](/docs/openshift?topic=openshift-acm&interface=ui#install-ui) onto your hub cluster. 
