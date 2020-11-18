---

copyright:
  years: 2014, 2020
lastupdated: "2020-11-17"

keywords: openshift, roks, rhoks, rhos, responsibilities, incident, operations, change, security, regulation, disaster recovery, management

subcollection: openshift

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
{:codeblock: .codeblock}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:fuzzybunny: .ph data-hd-programlang='fuzzybunny'}
{:generic: data-hd-operatingsystem="generic"}
{:generic: data-hd-programlang="generic"}
{:gif: data-image-type='gif'}
{:go: .ph data-hd-programlang='go'}
{:help: data-hd-content-type='help'}
{:hide-dashboard: .hide-dashboard}
{:hide-in-docs: .hide-in-docs}
{:important: .important}
{:ios: data-hd-operatingsystem="ios"}
{:java: #java .ph data-hd-programlang='java'}
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:new_window: target="_blank"}
{:note .note}
{:note: .note}
{:objectc data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:route: data-hd-keyref="route"}
{:row-headers: .row-headers}
{:ruby: .ph data-hd-programlang='ruby'}
{:ruby: data-hd-programlang="ruby"}
{:runtime: architecture="runtime"}
{:runtimeIcon: .runtimeIcon}
{:runtimeIconList: .runtimeIconList}
{:runtimeLink: .runtimeLink}
{:runtimeTitle: .runtimeTitle}
{:screen: .screen}
{:script: data-hd-video='script'}
{:service: architecture="service"}
{:service_instance_name: data-hd-keyref="service_instance_name"}
{:service_name: data-hd-keyref="service_name"}
{:shortdesc: .shortdesc}
{:space_name: data-hd-keyref="space_name"}
{:step: data-tutorial-type='step'}
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: #swift .ph data-hd-programlang='swift'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:tutorial: data-hd-content-type='tutorial'}
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vb.net: .ph data-hd-programlang='vb.net'}
{:video: .video}



# Your responsibilities with using {{site.data.keyword.openshiftlong_notm}}
{: #responsibilities_iks}
{: help}
{: support}

Learn about cluster management responsibilities that you have when you use {{site.data.keyword.openshiftlong}}. For overall terms of use, see [Cloud Services terms](/docs/overview/terms-of-use?topic=overview-terms#terms).
{: shortdesc}

## Overview of shared responsibilities
{: #overview-by-resource}

{{site.data.keyword.openshiftlong_notm}} is a managed service in the [{{site.data.keyword.cloud_notm}} shared responsibility model](/docs/overview/terms-of-use?topic=overview-shared-responsibilities). Review the following table of who is responsible for particular cloud resources when using {{site.data.keyword.openshiftlong_notm}}. Then, you can view more granular tasks for shared responsibilities in [Tasks for shared responsibilities by area](#task-responsibilities).
{: shortdesc}

If you use other {{site.data.keyword.cloud_notm}} products such as {{site.data.keyword.cos_short}}, responsibilities that are marked as yours in the following table, such as disaster recovery for Data, might be IBM's or shared. Consult those products' documentation for your responsibilities.
{: note}

| Resource | [Incident and operations management](#incident-and-ops) | [Change management](#change-management) | [Identity and access management](#iam-responsibilities) | [Security and regulation compliance](#security-compliance) | [Disaster Recovery](#disaster-recovery) |
| - | - | - | - | - | - |
| [Data](#applications-and-data) | You | You | You | You | You |
| [Applications](#applications-and-data) | You | You | You | You | You |
| Observability | [Shared](#incident-and-ops) | IBM | [Shared](#iam-responsibilities) | IBM | IBM |
| App networking | [Shared](#incident-and-ops) | IBM | IBM | IBM | IBM |
| Cluster networking | [Shared](#incident-and-ops) | IBM | IBM | IBM | IBM |
| Cluster version | IBM | [Shared](#change-management) | IBM | IBM | IBM |
| Worker nodes | [Shared](#incident-and-ops) | [Shared](#change-management) | IBM | IBM | IBM |
| Master | IBM | IBM | IBM | IBM | IBM |
| Service | IBM | IBM | IBM | IBM | IBM |
| Virtual storage | IBM | IBM | IBM | IBM | IBM |
| Virtual network | IBM | IBM | IBM | IBM | IBM |
| Hypervisor | IBM | IBM | IBM | IBM | IBM |
| Physical servers and memory | IBM | IBM | IBM | IBM | IBM |
| Physical storage | IBM | IBM | IBM | IBM | IBM |
| Physical network and devices | IBM | IBM | IBM | IBM | IBM |
| Facilities and Data Centers | IBM | IBM | IBM | IBM | IBM |
{: summary="The rows are read from left to right. The resource area of comparing responsibilities is in the first column. The next five columns describe whether you, IBM, or both have shared responsibilities for a particular area."}
{: caption="Table 1. Responsibilities by resource." caption-side="top"}

## Tasks for shared responsibilities by area
{: #task-responsibilities}

After reviewing the [overview](#overview-by-resource), see what tasks you and IBM share responsibility for each area and resource when you use {{site.data.keyword.openshiftlong_notm}}.
{: shortdesc}

### Incident and operations management
{: #incident-and-ops}

You and IBM share responsibilities for the set up and maintenance of your {{site.data.keyword.openshiftlong_notm}} cluster environment for your application workloads. You are responsible for incident and operations management of your application data.
{: shortdesc}

| Resource | IBM responsibilities | Your responsibilities |
| -------- | -------------------- | --------------------- |
| Worker nodes | <ul><li>Deploy a fully managed, highly available dedicated master in a secured, IBM-owned infrastructure account for each cluster.</li><li>Provision worker nodes in your IBM Cloud infrastructure account.</li><li>Ensure that worker nodes successfully provision when the user account and permissions are correctly set up, and sufficient quota exists.</li><li>Fulfill requests for more infrastructure, such as adding, reloading, updating, and removing worker nodes.</li><li>Provide tools, such as the [cluster autoscaler](/docs/openshift?topic=openshift-ca#ca), to extend your cluster infrastructure.</li><li>Integrate ordered infrastructure resources to work automatically with your cluster architecture and become available to your deployed apps and workloads.</li><li>Fulfill automation requests to help recover worker nodes.</li></ul> |<ul><li>Use the provided API, CLI, or console tools to adjust [compute](/docs/openshift?topic=openshift-add_workers) and [storage](/docs/openshift?topic=openshift-storage_planning) capacity to meet the needs of your workload.</li><li>Request that worker nodes are rebooted, reloaded, or replaced, and troubleshoot issues such as when the worker nodes are in an [unhealthy state](/docs/openshift?topic=openshift-cs_troubleshoot_clusters#debug_worker_nodes).</li></ul> |
| Cluster networking | <ul><li>Set up cluster management components, such as public or private service endpoints, VLANs, and load balancers.</li><li>Fulfill requests for more infrastructure, such as attaching worker nodes to existing VLANs or subnets upon resizing a worker pool.</li><li>Create clusters with subnet IP addresses reserved to use to expose apps externally.</li><li>Set up an OpenVPN connection between the master and worker nodes when the cluster is created.</li><li>Provide the ability to set up a VPN connection with on-premises resources such as through the strongSwan IPSec VPN service or the {{site.data.keyword.vpc_short}} VPN.</li><li>Provide the ability to isolate network traffic with edge nodes.</li></ul> | <ul><li>Use the provided API, CLI, or console tools to adjust [cluster networking configuration](/docs/openshift?topic=openshift-cs_network_cluster) to meet the needs of your workload, such as configuring service endpoints, adding VLANs to provide IP addresses for more worker nodes, setting up a VPN connection, or edge node worker pools.</li></ul> |
| App networking | <ul><li>Set up a public application load balancer (ALB) that is multizone, if applicable. Provide the ability to set up private ALBs and public or private network load balancers (NLBs).</li><li>Support native Kubernetes public and private load balancers and Ingress routes for exposing services externally.</li><li>Install Calico as the container networking interface, and set up default Calico network policies to control basic cluster traffic.</li></ul> | <ul><li>Set up any additional app networking capabilities that are needed, such as private ALBs, public or private NLBs, or additional Calico network policies.</li></ul>|
| Observability | <ul><li>Provide {{site.data.keyword.la_short}} and {{site.data.keyword.mon_short}} as managed add-ons to enable observability of your cluster and container environments. Maintenance is simplified for you because IBM provides the installation and updates for the managed add-ons.</li><li>Provide cluster integration with {{site.data.keyword.at_short}} and send {{site.data.keyword.openshiftlong_notm}} API events for auditability.</li></ul> | <ul><li>[Set up and monitor the health](/docs/containers?topic=containers-health) of your container logs and cluster metrics.</li><li>Set up and, if applicable, [configure `kube-audit` logs](/docs/containers?topic=containers-health#audit_enable) to be sent to [{{site.data.keyword.at_short}}](/docs/openshift?topic=openshift-at_events).</li></ul>|
{: summary="The rows are read from left to right. The resource area of comparing responsibilities is in the first column, with the responsibilities of IBM in the second column and your responsibilities in the third column."}
{: caption="Table 2. Responsibilities for incident and operations management" caption-side="top"}

<br />

### Change management
{: #change-management}

You and IBM share responsibilities for keeping your clusters at the latest container platform and operating system versions, along with recovering infrastructure resources that might require changes. You are responsible for change management of your application data.
{: shortdesc}

| Resource | IBM responsibilities | Your responsibilities |
| -------- | -------------------- | --------------------- |
| Worker nodes | <ul><li>Provide worker node patch operating system (OS), version, and security updates.</li><li>Fulfill automation requests to update and recover worker nodes.</li></ul> | <ul><li>Use the API, CLI, or console tools to [apply](/docs/openshift?topic=openshift-update#update) the provided worker node updates that include operating system patches; or to request that worker nodes are rebooted, reloaded, or replaced.</li></ul> |
| Cluster version | <ul><li>Provide a suite of tools to automate cluster management, such as the {{site.data.keyword.openshiftlong_notm}} [API](https://containers.cloud.ibm.com/global/swagger-global-api/#/){: external}, [CLI plug-in](/docs/openshift?topic=openshift-kubernetes-service-cli), and [console](https://cloud.ibm.com/kubernetes/clusters){: external}.</li><li>Automatically apply {{site.data.keyword.openshiftshort}} master patch OS, version, and security updates.</li><li>Make major and minor updates for master nodes available for you to apply.</li><li>Provide worker node major, minor, and patch OS, version, and security updates.</li><li>Fulfill automation requests to update cluster master and worker nodes.</li></ul> | <ul><li>Use the API, CLI, or console tools to [apply](/docs/openshift?topic=openshift-update#update) the provided major and minor {{site.data.keyword.openshiftshort}} master updates and major, minor, and patch worker node updates.</li></ul> |
{: summary="The rows are read from left to right. The resource area of comparing responsibilities is in the first column, with the responsibilities of IBM in the second column and your responsibilities in the third column."}
{: caption="Table 3. Responsibilities for change management" caption-side="top"}

<br />

### Identity and access management
{: #iam-responsibilities}

You and IBM share responsibilities for controlling access to your {{site.data.keyword.openshiftlong_notm}} instances. For {{site.data.keyword.iamlong}} responsibilities, consult that product's documentation. You are responsible for identity and access management to your application data.
{: shortdesc}

| Resource | IBM responsibilities | Your responsibilities |
| -------- | -------------------- | --------------------- |
| Observability | <ul><li>Provide the ability to integrate {{site.data.keyword.at_full_notm}} with your cluster to audit the actions that users take in the cluster.</li></ul> | <ul><li>Set up {{site.data.keyword.at_full_notm}} or other capabilities to track user activity in the cluster.</li></ul> |
{: summary="The rows are read from left to right. The resource area of comparing responsibilities is in the first column, with the responsibilities of IBM in the second column and your responsibilities in the third column."}
{: caption="Table 4. Responsibilities for identity and access management" caption-side="top"}

<br />

### Security and regulation compliance
{: #security-compliance}

IBM is responsible for the security and compliance of {{site.data.keyword.openshiftlong_notm}}. Compliance to industry standards varies depending on the infrastructure provider that you use for the cluster, such as classic or VPC. You are responsible for the security and compliance of any workloads that run in the cluster and your application data. For more information, see [What standards does the service comply to?](/docs/openshift?topic=openshift-faqs#standards).
{: shortdesc}

| Resource | IBM responsibilities | Your responsibilities |
| -------- | -------------------- | --------------------- |
| General | <ul><li>Maintain controls commensurate to [various industry compliance standards](/docs/openshift?topic=openshift-faqs#standards), such as PCI DSS. Compliance to industry standards varies depending on the infrastructure provider of the cluster, such as classic or VPC.</li><li>Monitor, isolate, and recover the cluster master.</li><li>Provide highly available replicas of the Kubernetes master API server, etcd, scheduler, and controller manager components to protect against a master outage.</li><li>Monitor and report the health of the master and worker nodes in the various interfaces.</li><li>Automatically apply master security patch updates, and provide worker node security patch updates.</li><li>Enable certain security settings, such as encrypted disks on worker nodes</li><li>Disable certain insecure actions for worker nodes, such as not permitting users to SSH into the host.</li><li>Encrypt communication between the master and worker nodes with TLS.</li><li>Provide CIS-compliant Linux images for worker node operating systems.</li><li>Continuously monitor master and worker node images to detect vulnerability and security compliance issues.</li><li>Provision worker nodes with two local SSD, AES 256-bit encrypted data partitions.</li><li>Provide options for cluster network connectivity, such as public and private service endpoints.</li><li>Provide options for compute isolation, such as dedicated virtual machines or bare metal.</li><li>Integrate Kubernetes role-based access control (RBAC) with {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM).</li></li></ul> | <ul><li>Set up and maintain security and regulation compliance for your apps and data. For example, choose how to set up your [cluster network](/docs/openshift?topic=openshift-plan_clusters), [protect sensitive information](/docs/openshift?topic=openshift-encryption) such as with {{site.data.keyword.keymanagementservicelong_notm}} encryption, and configure further [security settings](/docs/openshift?topic=openshift-security#security) to meet your workload's security and compliance needs. If applicable, configure your [firewall](/docs/openshift?topic=openshift-firewall#firewall).</li><li>As part of your incident and operations management responsibilities for the worker nodes, apply the provided security patch updates.</li></ul>  |
{: summary="The rows are read from left to right. The resource area of comparing responsibilities is in the first column, with the responsibilities of IBM in the second column and your responsibilities in the third column."}
{: caption="Table 5. Responsibilities for security and regulation compliance" caption-side="top"}

<br />

### Disaster recovery
{: #disaster-recovery}

IBM is responsible for the recovery of {{site.data.keyword.openshiftlong_notm}} components in case of disaster. You are responsible for the recovery of the workloads that run the cluster and your application data. If you integrate with other {{site.data.keyword.cloud_notm}} services such as file, block, object, cloud database, logging, or audit event services, consult those services' disaster recovery information.
{: shortdesc}

| Resource | IBM responsibilities | Your responsibilities |
| -------- | -------------------- | --------------------- |
| General | <ul><li>Maintain service availability across [worldwide locations](/docs/openshift?topic=openshift-regions-and-zones) so that customers can deploy clusters across zones and regions for higher DR tolerance.</li><li>Provision clusters with three replicas of master components for high availability.</li><li>In multizone regions, automatically spread the master replicas across zones.</li><li>Continuously monitor to work to ensure the reliability and availability of the service environment by site reliability engineers.</li><li>Update and recover operational {{site.data.keyword.openshiftlong_notm}} and Kubernetes components within the cluster, such as the Ingress application load balancer and file storage plug-in.</li><li>Back up and recover data in etcd, such as your Kubernetes workload configuration files</li><li>Provide the ability to integrate with other {{site.data.keyword.cloud_notm}} services such as storage providers so that data can be backed up and restored.</li></ul> | <ul><li>Set up and maintain disaster recovery capabilities for your apps and data. For example, to prepare your cluster for HA/DR scenarios, follow the guidance in [High availability for {{site.data.keyword.openshiftlong_notm}}](/docs/openshift?topic=openshift-ha). Note that persistent storage of data such as application logs and cluster metrics are not set up by default.</li></ul>  |
{: summary="The rows are read from left to right. The resource area of comparing responsibilities is in the first column, with the responsibilities of IBM in the second column and your responsibilities in the third column."}
{: caption="Table 6. Responsibilities for disaster recovery" caption-side="top"}

### Applications and data
{: #applications-and-data}

You are completely responsible for the applications, workloads, and data that you deploy to {{site.data.keyword.cloud_notm}}. However, IBM provides various tools to help you set up, manage, secure, integrate and optimize your apps as described in the following table.
{: shortdesc}

| Resource | How IBM helps | What you can do |
| -------- | -------------------- | --------------------- |
| Applications  |<ul><li>Provision clusters with {{site.data.keyword.openshiftshort}} components installed so that you can access the {{site.data.keyword.openshiftshort}} API to deploy and manage your containerized apps.</li><li>Provide a number of managed add-ons to extend your app's capabilities, such as the Diagnostics and Debug Tool. Maintenance is simplified for you because IBM provides the installation and updates for the managed add-ons.</li><li>Provide cluster integration with select third-party partnership technologies, such as {{site.data.keyword.la_short}}, {{site.data.keyword.mon_short}}, and Portworx.</li><li>Provide automation to enable service binding to other {{site.data.keyword.cloud_notm}} services.</li><li>Create clusters with image pull secrets so that your deployments in the `default` Kubernetes namespace can pull images from {{site.data.keyword.registrylong_notm}}.</li><li>Provide access to {{site.data.keyword.openshiftshort}} APIs that you can use to set up Operators to add community, third-party, and your own services to your cluster. Note that Operators might not work without manual adjustments such as changes in cluster security policies.</li><li>Provide storage classes and plug-ins to support persistent volumes for use with your apps.</li><li>Automatically configure security settings to prevent insecure access, such as disabling SSH into the worker node compute hosts.</li><li>Automatically integrate {{site.data.keyword.cloud_notm}} IAM service roles with Kubernetes RBAC roles in the cluster.</li><li>Generate an API key that is used to access infrastructure permissions for each resource group and region.</li></ul> | <ul><li>Maintain responsibility for your apps, data, and their complete lifecycle.</li><li>If you add community, third-party, your own, or other services to your cluster such as by using Operators, you are responsible for these services and for working with the appropriate provider to troubleshoot any issues.</li><li>Use the provided tools and features to [configure and deploy](/docs/openshift?topic=openshift-openshift_apps); [keep up-to-date](/docs/openshift?topic=openshift-update_app#app_rolling); [set up resource requests and limits](/docs/openshift?topic=openshift-openshift_apps#resourcereq); [size your worker pool](/docs/openshift?topic=openshift-strategy#sizing) to have enough resources to run your apps; [set up permissions](/docs/openshift?topic=openshift-users#users); [integrate with other services](/docs/openshift?topic=openshift-supported_integrations#supported_integrations); [manage any operators or templates that you deploy](/docs/openshift?topic=openshift-operators); [externally serve](/docs/containers?topic=containers-cs_network_planning#cs_network_planning); [save, back up, and restore data](/docs/openshift?topic=openshift-storage_planning#storage_planning); and otherwise manage your [highly available](/docs/openshift?topic=openshift-ha#ha) and resilient workloads.</li></ul> |
| Data | <ul><li>Maintain [platform-level standards](/docs/overview?topic=overview-security) so that your data can be stored with controls commensurate to leading international security compliance standards.</li><li>Provision clusters with {{site.data.keyword.openshiftshort}} components installed so that you can access the {{site.data.keyword.openshiftshort}} API to help manage your app data, such as with secrets and configmaps.</li><li>Integrate with {{site.data.keyword.cloud_notm}} services that you can use to store and manage your data, such as {{site.data.keyword.cloud_notm}} Databases or {{site.data.keyword.cos_short}}.</li><li>Integrate with {{site.data.keyword.ibmwatson_notm}} services that you can use to maximize the insights and use of your data with the latest artificial intelligence technology.</li></ul>| <ul><li>Maintain responsibility for your data and how your apps consume the data.</li></ul>
{: summary="The rows are read from left to right. The resource area of comparing responsibilities is in the first column, with the responsibilities of IBM in the second column and your responsibilities in the third column."}
{: caption="Table 7. Applications and data" caption-side="top"}


