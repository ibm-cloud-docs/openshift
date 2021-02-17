---

copyright:
  years: 2014, 2021
lastupdated: "2021-02-17"

keywords: openshift, roks, rhoks, rhos, http2, quota

subcollection: openshift

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:api: .ph data-hd-interface='api'}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
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
{:ui: .ph data-hd-interface='ui'}
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vbnet: .ph data-hd-programlang='vb.net'}
{:video: .video}



# Service limitations
{: #openshift_limitations}

{{site.data.keyword.openshiftlong}} and the {{site.data.keyword.openshiftshort}} open source project come with default service settings and limitations to ensure security, convenience, and basic functionality. Some of the limitations you might be able to change where noted.
{: shortdesc}
<br>

If you anticipate reaching any of the following {{site.data.keyword.openshiftlong_notm}} limitations, [contact IBM Support](/docs/get-support?topic=get-support-using-avatar) and provide the cluster ID, the new quota limit, and the region in your support ticket.
{: tip}

## Service and quota limitations
{: #tech_limits}

{{site.data.keyword.openshiftlong_notm}} comes with the following service limitations and quotas that apply to all clusters, independent of what infrastructure provider you plan to use. Keep in mind that the [classic](#classic_limits) and [VPC](#ks_vpc_gen2_limits) cluster limitations also apply.
{: shortdesc}

To view quota limits on cluster-related resources in your {{site.data.keyword.cloud_notm}} account, use the `ibmcloud oc quota ls` command.
{: tip}

| Category | Description |
| -------- | ----------- |
| API rate limits | 200 requests per 10 seconds to the {{site.data.keyword.openshiftlong_notm}} API from each unique source IP address. |
| App deployment | The apps that you deploy to and services that you integrate with your cluster must be able to run on the operating system of the worker nodes. |
| Cluster quota | You cannot exceed 100 clusters per region and per [infrastructure provider](/docs/openshift?topic=openshift-infrastructure_providers). If you need more of the resource, [contact IBM Support](/docs/get-support?topic=get-support-using-avatar). In the support case, include the new quota limit for the region and infrastructure provider that you want.|
| Free clusters | You can create only standard clusters, not free clusters. Instead, you can create a free Kubernetes cluster, and then redeploy the apps that you try out in the Kubernetes cluster to your {{site.data.keyword.openshiftshort}} cluster. |
| IAM access groups | You cannot scope {{site.data.keyword.cloud_notm}} IAM service access roles to an IAM access group because the roles are not synced to the RBAC roles within the cluster. If you want to scope RBAC roles to a group of users, you must [manually set up groups of users](https://docs.openshift.com/container-platform/4.5/authentication/understanding-authentication.html){: external} in your cluster instead of using IAM access groups. You can still manage individual users and service accounts with IAM service roles. You can also still scope IAM platform roles to IAM access groups to control actions like ordering worker nodes, because platform roles are never synced to RBAC roles. |
| Kubernetes | Make sure to review the [Kubernetes project limitations](https://kubernetes.io/docs/setup/best-practices/cluster-large/){: external}. |
| KMS provider | Customizing the IP addresses that are allowed to connect to your {{site.data.keyword.keymanagementservicefull}} instance is not supported. KMS provider integration is available only in version 3.11 or 4.4 clusters, not for version 4.3 clusters.|
| {{site.data.keyword.openshiftshort}} | Make sure to review the [OpenShift Container Platform limitations](https://docs.openshift.com/container-platform/4.5/scalability_and_performance/planning-your-environment-according-to-object-maximums.html){: external} for your version.|
| Kubernetes pod logs | To check the logs for individual app pods, you can use the command line to run `oc logs <pod name>`. Do not use the Kubernetes dashboard to stream logs for your pods, which might cause a disruption in your access to the Kubernetes dashboard. |
| Logging | <img src="images/icon-version-311.png" alt="Version 3.11 icon" width="30" style="width:30px; border-style: none"/> **{{site.data.keyword.openshiftshort}} 3.11 only**: <ul><li>You cannot run the Ansible playbook to deploy the [OpenShift Container Platform Elasticsearch, Fluentd, and Kibana (EFK) stack](https://docs.openshift.com/container-platform/3.11/install_config/aggregate_logging.html){: external} because you cannot modify the default configuration of the {{site.data.keyword.openshiftlong_notm}} cluster.</li><li>Collecting and forwarding API audit logs to {{site.data.keyword.la_full_notm}} is not supported.</li></ul> |
| Monitoring | <ul><li>Because IBM manages your cluster master, event alerting for the master is disabled. IBM monitors your cluster master and fixes issues as they are detected. For this reason, in the Administrator perspective of the {{site.data.keyword.openshiftshort}}, you might see a `Not available` message for the control plane status.</li><li>The built-in Prometheus alert manager includes two rules that display as active alerts in a `FIRING` state: `KubeControllerManagerDown` and `KubeSchedulerDown`. These components are part of the IBM-managed cluster master, so you can ignore these alerts.</li></ul>|
| {{site.data.keyword.openshiftshort}} Container Storage (OCS) | {{site.data.keyword.openshiftshort}} Container Storage is not supported. |
| Pod instances | You can run 110 pods per worker node. If you have worker nodes with 11 CPU cores or more, you can support 10 pods per core, up to a limit of 250 pods per worker node. The number of pods includes `kube-system` and `ibm-system` pods that run on the worker node. For improved performance, consider limiting the number of pods that you run per compute core so that you do not overuse the worker node. For example, on a worker node with a `b3c.4x16` flavor, you might run 10 pods per core that use no more than 75% of the worker node total capacity. |
| Time-based one-time passcode (TOTP) | To use [TOTP](/docs/account?topic=account-totp), make sure that you [enable multifactor authentication (MFA)](/docs/account?topic=account-enablemfa) for your entire {{site.data.keyword.cloud_notm}} account. |
| Worker node quota | You cannot exceed 500 worker nodes across all clusters in a region, per [infrastructure provider](/docs/openshift?topic=openshift-infrastructure_providers). If you need more of the resource, [contact IBM Support](/docs/get-support?topic=get-support-using-avatar). In the support case, include the new quota limit for the region and infrastructure provider that you want.|
| Worker pool size | You must have a minimum of 2 worker nodes in your cluster  at all times. Additionally, you cannot scale down a worker pool below 2 worker nodes per zone. For more information, see [What is the smallest size cluster that I can make?](/docs/openshift?topic=openshift-faqs#smallest_cluster). You cannot scale worker pools down to zero. Because of the worker node quota, you are limited in the number of worker pools per cluster and number of worker nodes per worker pool. For example, with the default worker node quota of 500 per region, you might have up to 500 worker pools of 1 worker node each in a region with only 1 cluster. Or, you might have 1 worker pool with up to 500 worker nodes in a region with only 1 cluster. |
{: summary="This table contains information on general {{site.data.keyword.openshiftlong_notm}} limitations. Columns are read from left to right. In the first column is the type of limitation and in the second column is the description of the limitation."}
{: caption="{{site.data.keyword.openshiftlong_notm}} limitations"}

<br />



### Version 4 cluster limitations
{: #ocp4_limitations}

Review limitations that are specific to {{site.data.keyword.openshiftshort}} version 4 clusters. Keep in mind that the [service](#tech_limits) and [classic cluster](#classic_limits) or [VPC cluster](#ks_vpc_gen2_limits) limitations also apply.
{: shortdesc}

| Category | Description |
| -------- | ----------- |
| Cluster autoscaling | The Red Hat {{site.data.keyword.openshiftshort}} cluster autoscaler from the {{site.data.keyword.openshiftshort}} **Administration > Cluster Settings** console or `ClusterAutoscaler` object from the `autoscaling.openshift.io/v1` API is not supported. Instead, use the [`ibm-iks-cluster-autoscaler` Helm plug-in](/docs/openshift?topic=openshift-ca). |
| Cluster updates | You must [update your cluster](/docs/openshift?topic=openshift-update) by using the {{site.data.keyword.openshiftlong_notm}} API, CLI, or console tools. You cannot update your cluster version from OpenShift Container Platform tools such as the {{site.data.keyword.openshiftshort}} web console. |
| Container logs | If you use a container logging operator such as Fluentd to send logs to an ElasticSearch stack, you must [update the cluster logging deployment to use the `ibmc-block-gold` storage class](/docs/openshift?topic=openshift-health#oc_logging_operator).|
| Key management service (KMS) provider | You can use a KMS provider such as {{site.data.keyword.keymanagementservicelong}} to encrypt secrets in your cluster only in clusters that run version 4.4 or later, not in clusters that run version 4.3. |
| Private clusters | Depending on the infrastructure provider, your options for private clusters are limited.<ul><li><img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> **VPC**: When you create your VPC cluster in the {{site.data.keyword.cloud_notm}} console, your cluster has both a public and a private service endpoint. If you want only a private service endpoint, you must create the cluster [in the CLI](/docs/openshift?topic=openshift-clusters#cluster_vpcg2_cli) instead, and include the `--disable-public-service-endpoint` flag. If you include this flag, your cluster is created with routers and Ingress controllers that expose your apps on the private network only by default. If you later want to expose apps to a public network, you must manually create public routers and Ingress controllers.</li><li>**Classic**: You cannot enable the private service endpoint in classic version 4 clusters. Classic version 4 clusters are created with the public service endpoint only, and you cannot later change the service endpoints.</li></ul> |
| Logging | To set up an [OpenShift Container Platform Elasticsearch, Fluentd, and Kibana (EFK) stack](https://docs.openshift.com/container-platform/4.5/logging/cluster-logging.html){: external}, see [installing the cluster logging operator](/docs/openshift?topic=openshift-health#oc_logging_operator).|
| Service catalog | The service catalog is not supported. Use [Operators](/docs/openshift?topic=openshift-operators#operators_4) instead. Do not use the OperatorHub to install the service catalog. |
| Service mesh | The Istio managed add-on is not supported. Instead, use the [Red Hat service mesh operator](https://docs.openshift.com/container-platform/4.5/service_mesh/v1x/servicemesh-release-notes.html){: external}. **Note**: The default {{site.data.keyword.cloud_notm}} configuration of the routers enables host networking, which is not compatible with the service mesh network policy. For the service mesh ingress to work, [apply a network policy](https://gist.githubusercontent.com/kitch/39c504a2ed9e381c2aadea436d5b52e4/raw/d8efa69f41d41425b16bb363a881a98d40d3708c/mesh-policy.yaml){: external}.|
{: summary="This table contains information on limitations for OpenShift Container Platform version 4 clusters. Columns are read from left to right. In the first column is the type of limitation and in the second column is the description of the limitation."}
{: caption="OpenShift Container Platform version 4 cluster limitations"}




## Classic cluster limitations
{: #classic_limits}

<img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic infrastructure clusters in {{site.data.keyword.openshiftlong_notm}} are released with the following limitations.
{: shortdesc}

### Compute
{: #classic_compute_limit}

Keep in mind that the [service](#tech_limits) limitations also apply.

| Category | Description |
| -------- | ----------- |
| Operating system | You cannot create a cluster with worker nodes that run multiple operating systems, such as {{site.data.keyword.openshiftshort}} on Red Hat Enterprise Linux and community Kubernetes on Ubuntu. |
| Reserved instances | [Reserved capacity and reserved instances](/docs/virtual-servers?topic=virtual-servers-provisioning-reserved-capacity-and-instances) are not supported. |
| Worker node flavors | Worker nodes are available in [select flavors](/docs/openshift?topic=openshift-planning_worker_nodes#shared_dedicated_node) of compute resources. |
| Worker node host access | For security, you cannot SSH into the worker node compute host. |
{: summary="This table contains information on compute limitations for classic clusters. Columns are read from left to right. In the first column is the type of limitation and in the second column is the description of the limitation."}
{: caption="Classic cluster compute limitations"}

### Networking
{: #classic_networking_limit}

Keep in mind that the [service](#tech_limits) limitations also apply.

| Category | Description |
| -------- | ----------- |
| Ingress ALBs | <ul><li>The Ingress application load balancer (ALB) can process 32,768 connections per second. If your Ingress traffic exceeds this number, [scale up the number of ALB replicas](/docs/containers?topic=containers-ingress#scale_albs) in your cluster to handle the increased workload.</li><li>ALBs that run the [{{site.data.keyword.openshiftlong_notm}} custom Ingress image](/docs/containers?topic=containers-ingress-types) only: HTTP/2 is not supported.</li><li>ALBs that run the [{{site.data.keyword.openshiftlong_notm}} custom Ingress image](/docs/containers?topic=containers-ingress-types) only: The names of the `ClusterIP` services that expose your apps must be unique across all namespaces in your cluster.</li></ul> |
| Network load balancers (NLB)| <ul><li>You cannot create version 2.0 network load balancers (NLB 2.0) to expose your apps.</li><li>You cannot create subdomains for private NLBs.</li><li>You can register up to 128 subdomains. This limit can be lifted on request by opening a [support case](/docs/get-support?topic=get-support-using-avatar).</li></ul> | 
| Private VLANs only | Private network load balancers (NLBs) cannot be registered with the domain name server (DNS), so the cluster cannot be created with only a private network interface. Worker nodes must be connected to both public and private VLANs. You can still create a private service to expose your apps on only the private network. |
| Service endpoints | When you create a cluster, you must enable the public service endpoint, and you cannot later disable the public service endpoint. In version 3.11 clusters, you can optionally enable the private service endpoint. In version 4 classic clusters, you cannot enable the private service endpoint. | 
| strongSwan VPN service | See [strongSwan VPN service considerations](/docs/openshift?topic=openshift-vpn#strongswan_limitations). |
| Service IP addresses | You can have 65,000 IP addresses per cluster in the 172.21.0.0/16 range that you can assign to Kubernetes services within the cluster. |
| Subnets per VLAN | Each VLAN has a limit of 40 subnets. |
{: summary="This table contains information on networking limitations for classic clusters. Columns are read from left to right. In the first column is the type of limitation and in the second column is the description of the limitation."}
{: caption="Classic cluster networking limitations"}

### Storage
{: #classic_storage_limit}

Keep in mind that the [service](#tech_limits) limitations also apply.

| Category | Description |
| -------- | ----------- |
| Volume instances | You can have a total of 250 IBM Cloud infrastructure file and block storage volumes per account. If you mount more than this amount, you might see an "out of capacity" message when you provision persistent volumes. For more FAQs, see the [file](/docs/FileStorage?topic=FileStorage-file-storage-faqs#provision) and [block](/docs/BlockStorage?topic=BlockStorage-block-storage-faqs#authlimit) storage docs. If you want to mount more volumes, [contact IBM Support](/docs/get-support?topic=get-support-using-avatar). In your support ticket, include your account ID and the new file or block storage volume quota that you want.  |
| Portworx | Review the [Portworx limitations](/docs/openshift?topic=openshift-portworx#portworx_limitations). |
| File storage | Because of the way that {{site.data.keyword.cloud_notm}} NFS file storage configures Linux user permissions, you might encounter errors when you use file storage. If so, you might need to configure [{{site.data.keyword.openshiftshort}} Security Context Constraints](https://docs.openshift.com/container-platform/4.5/authentication/managing-security-context-constraints.html){: external} or use a different storage type. |
{: summary="This table contains information on storage limitations for classic clusters. Columns are read from left to right. In the first column is the type of limitation and in the second column is the description of the limitation."}
{: caption="Classic cluster storage limitations"}

<br />

## VPC Gen 2 compute cluster limitations
{: #ks_vpc_gen2_limits}

<img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> <img src="images/icon-vpc-gen2.png" alt="VPC Generation 2 compute icon" width="30" style="width:30px; border-style: none"/> VPC Generation 2 compute clusters in {{site.data.keyword.openshiftlong_notm}} are released with the following limitations. Additionally, all the underlying [VPC quotas, VPC limits](/docs/vpc?topic=vpc-quotas), [VPC service limitations](/docs/vpc?topic=vpc-limitations), and [regular service limitations](#tech_limits) apply.
{: shortdesc}

### Compute
{: #vpc_gen2_compute_limit}

Keep in mind that the [service](#tech_limits) limitations also apply.

| Category | Description |
| -------- | ----------- |
| Encryption | The secondary disks of your worker nodes are encrypted at rest by default by the [underlying VPC infrastructure provider](/docs/vpc?topic=vpc-block-storage-about#vpc-storage-encryption). However, you cannot [bring your own encryption to the underlying virtual server instances](/docs/vpc?topic=vpc-creating-instances-byok).|
| Location | VPC Gen 2 clusters are available only in [select multizone metro locations](/docs/openshift?topic=openshift-regions-and-zones#zones-vpc-gen2). |
| Operating system | You cannot create a cluster with worker nodes that run multiple operating systems, such as {{site.data.keyword.openshiftshort}} on Red Hat Enterprise Linux and community Kubernetes on Ubuntu. |
| Versions | VPC Gen 2 clusters must run {{site.data.keyword.openshiftshort}} version 4.3 or later. |
| Virtual Private Cloud | See [Known limitations](/docs/vpc-on-classic?topic=vpc-on-classic-known-limitations) and [Quotas](/docs/vpc-on-classic?topic=vpc-on-classic-quotas). |
| v2 API | VPC clusters use the [{{site.data.keyword.openshiftlong_notm}} v2 API](/docs/openshift?topic=openshift-cs_api_install#api_about). The v2 API is currently under development, with only a limited number of API operations currently available. You can run certain v1 API operations against the VPC cluster, such as `GET /v1/clusters` or `ibmcloud oc cluster ls`, but not all the information that a Classic cluster has is returned or you might experience unexpected results. For supported VPC v2 operations, see the [CLI reference topic for VPC commands](/docs/openshift?topic=openshift-kubernetes-service-cli#cli_classic_vpc_about). |
| Worker node flavors | Only certain flavors are available for worker node [virtual machines](/docs/openshift?topic=openshift-planning_worker_nodes#vm). Bare metal machines are not supported.|
| Worker node host access | For security, you cannot SSH into the worker node compute host. |
| Worker node updates | You cannot update or reload worker nodes. Instead, you can delete the worker node and rebalance the worker pool with the `ibmcloud oc worker replace` command. If you replace multiple worker nodes at the same time, they are deleted and replaced concurrently, not one by one. Make sure that you have enough capacity in your cluster to reschedule your workloads before you replace worker nodes. |
{: summary="This table contains information on compute limitations for VPC Gen 2 clusters. Columns are read from left to right. In the first column is the type of limitation and in the second column is the description of the limitation."}
{: caption="VPC Gen 2 cluster compute limitations"}


### Networking
{: #vpc_gen2_networking_limit}

Keep in mind that the [service](#tech_limits) limitations also apply.

| Category | Description |
| -------- | ----------- |
| Network speeds | [VPC Gen 2 compute profile network speeds](/docs/vpc?topic=vpc-profiles) refer to the speeds of the worker node interfaces. The maximum speed available to your worker nodes is `16Gbps`. Because IP in IP encapsulation is required for traffic between pods that are on different VPC Gen 2 worker nodes, data transfer speeds between pods on different worker nodes might be slower, about half the compute profile network speed. Overall network speeds for apps that you deploy to your cluster depend on the worker node size and application's architecture. |
| NodePort | You can access an app through a NodePort only if you are connected to your private VPC network, such as through a VPN connection. To access an app from the internet, you must use a VPC load balancer or Ingress service instead. |
| Pod network | VPC access control lists (ACLs) filter incoming and outgoing traffic for your cluster at the subnet level, and security groups filter incoming and outgoing traffic for your cluster at the worker nodes level. To control traffic within the cluster at the pod-to-pod level, you cannot use VPC security groups or ACLs. Instead, use [Calico](/docs/openshift?topic=openshift-network_policies) and [Kubernetes network policies](/docs/openshift?topic=openshift-vpc-network-policy#kubernetes_policies), which can control the pod-level network traffic that uses IP in IP encapsulation. |
| Public gateway | You must attach a public gateway to each VPC subnet so that so that your worker nodes can communicate on the public network. Default {{site.data.keyword.openshiftshort}} components, such as the web console and OperatorHub, require public network access. If you do not attach a public gateway to your subnets, you must instead be connected to your VPC private network, such as through a VPN connection, to access the {{site.data.keyword.openshiftshort}} web console or access your cluster with `kubectl` commands.|
| Router health checks | If you set up [VPC security groups](/docs/openshift?topic=openshift-vpc-network-policy#security_groups) or [VPC access control lists (ACLs)](/docs/openshift?topic=openshift-vpc-network-policy#acls) to secure your cluster network, the necessary inbound access for router health checks is blocked. The {{site.data.keyword.openshiftshort}} control plane IP addresses are blocked from checking the health and reporting the overall status of your Ingress components. The Cloudflare IPv4 IP addresses are blocked from checking the health of the IP addresses of your router services. Because each ACL has a quota of only 50 rules and each security group has a quota of only 25 rules, you currently cannot add enough inbound and outbound rules for each {{site.data.keyword.openshiftshort}} control plane and Cloudflare IP address. Due to this known limitation your Ingress status shows that your routers are unreachable; however, this status does not reflect your router services' actual health. |
| Service endpoints | When you create your VPC cluster in the {{site.data.keyword.cloud_notm}} console, your cluster has both a public and a private service endpoint. If you want only a private service endpoint, you must create the cluster [in the CLI](/docs/openshift?topic=openshift-clusters#cluster_vpcg2_cli) instead, and include the `--disable-public-service-endpoint` flag. If you include this flag, your cluster is created with routers and Ingress controllers that expose your apps on the private network only by default. If you later want to expose apps to a public network, you must manually create public routers and Ingress controllers.|
| strongSwan VPN service | The strongSwan service is not supported. To connect your cluster to resources in an on-premises network or another VPC, see [Using VPN with your VPC](/docs/vpc?topic=vpc-vpn-onprem-example). |
| Subnets | <ul><li>See [VPC networking limitations](/docs/openshift?topic=openshift-vpc-subnets#vpc_basics_limitations).</li><li>Do not delete the subnets that you attach to your cluster during cluster creation or when you add worker nodes in a zone. If you delete a VPC subnet that your cluster used, any load balancers that use IP addresses from the subnet might experience issues, and you might be unable to create new load balancers.</li></ul> |
| VPC load balancer | See [VPC load balancer limitations](/docs/openshift?topic=openshift-vpc-lbaas#lbaas_limitations). |
| VPC security groups | VPC Gen 2 clusters that run {{site.data.keyword.openshiftshort}} version 4.4 or earlier only: You must [allow inbound traffic requests to node ports on your worker nodes](/docs/openshift?topic=openshift-vpc-network-policy#security_groups). |
{: summary="This table contains information on networking limitations for VPC Gen 2 clusters. Columns are read from left to right. In the first column is the type of limitation and in the second column is the description of the limitation."}
{: caption="VPC Gen 2 cluster networking limitations"}

### Storage
{: #vpc_gen2_storage_limit}

Keep in mind that the [service](#tech_limits) limitations also apply.

| Category | Description |
| -------- | ----------- |
| Storage class for profile sizes | The [available volume profiles](/docs/vpc?topic=vpc-block-storage-profiles) are limited to 2TB in size and 20,000 IOPS in capacity. |
| Supported types | You can set up {{site.data.keyword.cos_full_notm}} and {{site.data.keyword.databases-for}} only. |
| Unsupported types | NFS File Storage and {{site.data.keyword.block_storage_is_short}} are not supported. |
| Volume attachments | See [Volume attachment limits](/docs/vpc?topic=vpc-attaching-block-storage#vol-attach-limits).|
| Portworx | Review the [Portworx limitations](/docs/openshift?topic=openshift-portworx#portworx_limitations). |
{: summary="This table contains information on storage limitations for VPC Gen 2 clusters. Columns are read from left to right. In the first column is the type of limitation and in the second column is the description of the limitation."}
{: caption="VPC Gen 2 cluster storage limitations"}





## {{site.data.keyword.satelliteshort}} cluster limitations
{: #satellite_limits}

Review the following limitations for [{{site.data.keyword.openshiftlong_notm}} clusters that you create in a {{site.data.keyword.satelliteshort}} location](/docs/openshift?topic=openshift-satellite-clusters). Keep in mind that the [service](#tech_limits) limitations also apply.
{: shortdesc}

| Category | Description |
| -------- | ----------- |
| Cluster autoscaler | The [cluster autoscaler](/docs/openshift?topic=openshift-ca) is not supported.|
| Key management service (KMS) | Cluster integration with a key management service (KMS) provider like {{site.data.keyword.keymanagementserviceshort}} is not supported.|
| Locations | You must create your own [{{site.data.keyword.satelliteshort}} location](/docs/satellite?topic=satellite-locations) that is managed from [select {{site.data.keyword.cloud_notm}} multizone metros](/docs/satellite?topic=satellite-sat-regions). |
| Logging and monitoring | You cannot currently use the {{site.data.keyword.openshiftlong_notm}} console or the observability plug-in CLI (`ibmcloud ob`) to enable logging and monitoring for {{site.data.keyword.satelliteshort}} clusters. Instead, you can manually deploy [LogDNA agents](/docs/Log-Analysis-with-LogDNA?topic=Log-Analysis-with-LogDNA-kube#kube) and [Sysdig agents](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-kubernetes_cluster#kubernetes_cluster) to your cluster to forward logs and metrics to {{site.data.keyword.la_full_notm}} and {{site.data.keyword.mon_full_notm}}. |
| Network | <ul><li>The private service endpoint is not supported for {{site.data.keyword.satelliteshort}} clusters.</li><li>Your {{site.data.keyword.satelliteshort}} clusters cannot use Kubernetes load balancers.</li><li>The hosts that run the worker nodes for your cluster must meet the [host networking](/docs/satellite?topic=satellite-host-reqs#reqs-host-network) and [provider-specific](/docs/satellite?topic=satellite-providers) requirements. For example, depending on your provider, you might have to manually register the host IP addresses in the DNS for the location or cluster subdomains.</li></ul>|
| Storage for worker node hosts | See [Host storage and attached devices](/docs/satellite?topic=satellite-host-reqs#reqs-host-storage). |
| Storage for apps | <ul><li>No location-wide storage solution is provided to store your application data.</li><li>No storage provider is installed in your {{site.data.keyword.satelliteshort}} clusters by default. Therefore, no pre-configured Kubernetes storage classes are set up by default in your clusters to store your application data in a Kubernetes persistent volume that is backed by storage device.</li><li>You can [install your own storage driver in your {{site.data.keyword.satelliteshort}} clusters](/docs/openshift?topic=openshift-satellite-clusters#satcluster-storage) to store your application data in Kubernetes persistent volumes that are backed by a storage provider.</li></ul> |
| Worker nodes | Worker nodes run on hosts in your own infrastructure environments. The hosts must meet [host](/docs/satellite?topic=satellite-host-reqs) and [provider-specific](/docs/satellite?topic=satellite-providers) requirements. You are responsible for [managing the lifecycle of your hosts](/docs/satellite?topic=satellite-hosts), including adding and updating worker nodes. As such, operations such as `ibmcloud oc worker update, replace, reload` commands are not supported. |
| Worker pools | When you assign hosts to a {{site.data.keyword.satelliteshort}} cluster, the hosts are added to the `default` worker pool. You cannot add, resize, rebalance, or delete worker pools. |
{: summary="This table contains information on storage limitations for {{site.data.keyword.satelliteshort}} clusters. Columns are read from left to right. In the first column is the type of limitation and in the second column is the description of the limitation."}
{: caption="{{site.data.keyword.satelliteshort}} cluster limitations"}





