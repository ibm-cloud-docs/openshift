---

copyright: 
  years: 2014, 2022
lastupdated: "2022-03-10"

keywords: openshift, http2, quota, app protocol, application protocol

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}

# Service limitations
{: #openshift_limitations}

{{site.data.keyword.openshiftlong}} and the {{site.data.keyword.redhat_openshift_notm}} open source project come with default service settings and limitations to ensure security, convenience, and basic functionality. Some of the limitations you might be able to change where noted.
{: shortdesc}


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
| Container-native virtualization | The {{site.data.keyword.redhat_openshift_notm}} [container-native virtualization add-on](https://docs.openshift.com/container-platform/4.8/virt/about-virt.html){: external} to run VM workloads alongside container workloads is not supported by IBM. If you choose to install the add-on yourself, you must use bare metal machines, not virtual machines. You are responsible for resolving any issues and impact to your workloads from using container-native virtualization.|
| Calico network plug-in | Changing the Calico plug-in, components, or default Calico settings is not supported. For example, don't deploy a new Calico plug-in version, or modify the daemon sets or deployments for the Calico components, default `IPPool` resources, or Calico nodes. Instead, you can follow the documentation to [create a Calico `NetworkPolicy` or `GlobalNetworkPolicy`](/docs/containers?topic=containers-network_policies), to [change the Calico MTU](/docs/openshift?topic=openshift-kernel#calico-mtu), or to [disable the port map plug-in for the Calico CNI](/docs/openshift?topic=openshift-kernel#calico-portmap). |
| Cluster quota | You can't exceed 100 clusters per region and per [infrastructure provider](/docs/containers?topic=containers-infrastructure_providers). If you need more of the resource, [contact IBM Support](/docs/get-support?topic=get-support-using-avatar). In the support case, include the new quota limit for the region and infrastructure provider that you want.|
| Free clusters | You can create only standard clusters, not free clusters. Instead, you can create a free Kubernetes cluster, and then redeploy the apps that you try out in the Kubernetes cluster to your {{site.data.keyword.redhat_openshift_notm}} cluster. |
| IAM access groups | You can't scope {{site.data.keyword.cloud_notm}} IAM service access roles to an IAM access group because the roles are not synced to the RBAC roles within the cluster. If you want to scope RBAC roles to a group of users, you must [manually set up groups of users](https://docs.openshift.com/container-platform/4.8/authentication/understanding-authentication.html){: external} in your cluster instead of using IAM access groups. You can still manage individual users and service accounts with IAM service access roles. You can also still scope IAM platform access roles to IAM access groups to control actions like ordering worker nodes, because platform access roles are never synced to RBAC roles. |
| Kubernetes | Make sure to review the [Kubernetes project limitations](https://kubernetes.io/docs/setup/best-practices/cluster-large/){: external}. |
| KMS provider | Customizing the IP addresses that are allowed to connect to your {{site.data.keyword.keymanagementservicefull}} instance is not supported.|
| {{site.data.keyword.redhat_openshift_notm}} | Make sure to review the [OpenShift Container Platform limitations](https://docs.openshift.com/container-platform/4.8/scalability_and_performance/planning-your-environment-according-to-object-maximums.html){: external} for your version.|
| Kubernetes pod logs | To check the logs for individual app pods, you can use the command line to run `oc logs <pod name>`. Do not use the Kubernetes dashboard to stream logs for your pods, which might cause a disruption in your access to the Kubernetes dashboard. |
| Logging | ![Version 3.11 icon.](images/icon-version-311.png) **{{site.data.keyword.redhat_openshift_notm}} 3.11 only**: You can't run the Ansible playbook to deploy the  [OpenShift Container Platform Elasticsearch, Fluentd, and Kibana (EFK) stack](https://docs.openshift.com/container-platform/3.11/install_config/aggregate_logging.html){: external} because you can't modify the default configuration of the {{site.data.keyword.openshiftlong_notm}} cluster. In addition, collecting and forwarding API audit logs to {{site.data.keyword.la_full_notm}} is not supported.  |
| Monitoring |  - Because IBM manages your cluster master, event alerting for the master is disabled. IBM monitors your cluster master and fixes issues as they are detected. For this reason, in the Administrator perspective of the {{site.data.keyword.redhat_openshift_notm}}, you might see a `Not available` message for the control plane status. \n - The built-in Prometheus alert manager includes two rules that display as active alerts in a `FIRING` state: `KubeControllerManagerDown` and `KubeSchedulerDown`. These components are part of the IBM-managed cluster master, so you can ignore these alerts. |
| Operating system | Worker nodes must run RHEL 7. You can't create a cluster with worker nodes that run different types of operating systems, such as {{site.data.keyword.redhat_openshift_notm}} on Red Hat Enterprise Linux and community Kubernetes on Ubuntu.|
| OperatorHub catalog | To use the OperatorHub catalog in private clusters that run {{site.data.keyword.redhat_openshift_notm}} version 4.6 or later, see [Disabling and mirroring OperatorHub catalog source images](/docs/openshift?topic=openshift-operators#mirror-operatorhub). |
| Pod instances | You can run 110 pods per worker node. If you have worker nodes with 11 CPU cores or more, you can support 10 pods per core, up to a limit of 250 pods per worker node. The number of pods includes `kube-system` and `ibm-system` pods that run on the worker node. For improved performance, consider limiting the number of pods that you run per compute core so that you don't overuse the worker node. For example, on a worker node with a `b3c.4x16` flavor, you might run 10 pods per core that use no more than 75% of the worker node total capacity. |
| Time-based one-time passcode (TOTP) | To use [TOTP](/docs/account?topic=account-totp), make sure that you [enable multifactor authentication (MFA)](/docs/account?topic=account-enablemfa) for your entire {{site.data.keyword.cloud_notm}} account. If MFA is enabled only for some users but not at the account level, authentication errors might occur.  |
| Worker node quota | You can't exceed 500 worker nodes across all clusters in a region, per [infrastructure provider](/docs/containers?topic=containers-infrastructure_providers). If you need more of the resource, [contact IBM Support](/docs/get-support?topic=get-support-using-avatar). In the support case, include the new quota limit for the region and infrastructure provider that you want.|
| Worker pool size | You must always have a minimum of 2 worker nodes in your cluster . Additionally, you can't scale down a worker pool below 2 worker nodes per zone. For more information, see [What is the smallest size cluster that I can make?](/docs/openshift?topic=openshift-faqs#smallest_cluster). You can't scale worker pools down to zero. Because of the worker node quota, you are limited in the number of worker pools per cluster and number of worker nodes per worker pool. For example, with the default worker node quota of 500 per region, you might have up to 500 worker pools of 1 worker node each in a region with only 1 cluster. Or, you might have 1 worker pool with up to 500 worker nodes in a region with only 1 cluster. |
{: caption="{{site.data.keyword.openshiftlong_notm}} limitations"}





### Version 4 cluster limitations
{: #ocp4_limitations}

Review limitations that are specific to {{site.data.keyword.redhat_openshift_notm}} version 4 clusters. Keep in mind that the [service](#tech_limits) and [classic cluster](#classic_limits) or [VPC cluster](#ks_vpc_gen2_limits) limitations also apply.
{: shortdesc}

| Category | Description |
| -------- | ----------- |
| Cluster autoscaling | The Red Hat {{site.data.keyword.redhat_openshift_notm}} cluster autoscaler from the {{site.data.keyword.redhat_openshift_notm}} **Administration > Cluster Settings** console or `ClusterAutoscaler` object from the `autoscaling.openshift.io/v1` API is not supported. Instead, use the [`ibm-iks-cluster-autoscaler` Helm plug-in](/docs/openshift?topic=openshift-cluster-scaling-classic-vpc). |
| Cluster updates | You must [update your cluster](/docs/openshift?topic=openshift-update) by using the {{site.data.keyword.openshiftlong_notm}} API, CLI, or console tools. You can't update your cluster version from OpenShift Container Platform tools such as the {{site.data.keyword.redhat_openshift_notm}} web console. |
| Container logs | If you use a container logging operator such as Fluentd to send logs to an ElasticSearch stack, you must [update the cluster logging deployment to use the `ibmc-block-gold` storage class](/docs/openshift?topic=openshift-health#oc_logging_operator). |
| Private clusters | Depending on the infrastructure provider, your options for private clusters are limited. \n - **VPC**: When you create your VPC cluster in the {{site.data.keyword.cloud_notm}} console, your cluster has both a public and a private cloud service endpoint. If you want only a private cloud service endpoint, you must create the cluster [in the CLI](/docs/openshift?topic=openshift-clusters#cluster_vpcg2_cli) instead, and include the `--disable-public-service-endpoint` flag. If you include this flag, your cluster is created with routers and Ingress controllers that expose your apps on the private network only by default. If you later want to expose apps to a public network, you must manually create public routers and Ingress controllers. \n - **Classic**: You can enable the public and private cloud service endpoint or the public cloud service endpoint only, but you can't enable the private cloud service endpoint only. After cluster creation, you can't later change the service endpoints.  |
| Logging | To set up an [OpenShift Container Platform Elasticsearch, Fluentd, and Kibana (EFK) stack](https://docs.openshift.com/container-platform/4.8/logging/cluster-logging.html){: external}, see [installing the cluster logging operator](/docs/openshift?topic=openshift-health#oc_logging_operator).|
| Service catalog | The service catalog is not supported. Use [Operators](/docs/openshift?topic=openshift-operators#operators_4) instead. Do not use the OperatorHub to install the service catalog. |
| Service mesh | The Istio managed add-on is not supported. Instead, use the [Red Hat service mesh operator](https://docs.openshift.com/container-platform/4.8/service_mesh/v1x/servicemesh-release-notes.html){: external}. **Note**: The default {{site.data.keyword.cloud_notm}} configuration of the routers enables host networking, which is not compatible with the service mesh network policy. For the service mesh ingress to work, [apply a network policy](https://gist.githubusercontent.com/kitch/39c504a2ed9e381c2aadea436d5b52e4/raw/d8efa69f41d41425b16bb363a881a98d40d3708c/mesh-policy.yaml){: external}.|
{: caption="OpenShift Container Platform version 4 cluster limitations"}




## Classic cluster limitations
{: #classic_limits}

![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic infrastructure clusters in {{site.data.keyword.openshiftlong_notm}} are released with the following limitations.
{: shortdesc}

### Compute
{: #classic_compute_limit}

Keep in mind that the [service](#tech_limits) limitations also apply.

| Category | Description |
| -------- | ----------- |
| Reserved instances | [Reserved capacity and reserved instances](/docs/virtual-servers?topic=virtual-servers-provisioning-reserved-capacity-and-instances) are not supported. |
| Worker node flavors | Worker nodes are available in [select flavors](/docs/openshift?topic=openshift-planning_worker_nodes#shared_dedicated_node) of compute resources. |
| Worker node host access | For security, you can't SSH into the worker node compute host. |
{: caption="Classic cluster compute limitations"}

### Networking
{: #classic_networking_limit}

Keep in mind that the [service](#tech_limits) limitations also apply.

| Category | Description |
| -------- | ----------- |
| Ingress ALBs |  \n - The Ingress application load balancer (ALB) can process 32,768 connections per second. If your Ingress traffic exceeds this number,  [scale up the number of ALB replicas](/docs/containers?topic=containers-ingress-types#scale_albs) in your cluster to handle the increased workload. \n - ALBs that run the [{{site.data.keyword.openshiftlong_notm}} custom Ingress image](/docs/containers?topic=containers-ingress-types) only: HTTP/2 is not supported. \n - ALBs that run the [{{site.data.keyword.openshiftlong_notm}} custom Ingress image] (/docs/containers?topic=containers-ingress-types) only: The names of the `ClusterIP` services that expose your apps must be unique across all namespaces in your cluster.  |
| Network load balancers (NLB)| - You can't create version 2.0 network load balancers (NLB 2.0) to expose your apps. \n - You can't create subdomains for private NLBs. \n - You can register up to 128 subdomains. This limit can be lifted on request by opening a [support case](/docs/get-support?topic=get-support-using-avatar).  | 
| {{site.data.keyword.redhat_openshift_notm}} web console | The web console cannot be exposed on the private network on clusters that have both public and private endpoints. If you want to expose the web console on the private network, you cluster cannot have a public endpoint enabled.  | 
| Private VLANs only | Private network load balancers (NLBs) can't be registered with the domain name server (DNS), so the cluster can't be created with only a private network interface. Worker nodes must be connected to both public and private VLANs. You can still create a private service to expose your apps on only the private network. |
| Service endpoints | When you create a cluster, you can enable the public and private cloud service endpoint or the public cloud service endpoint only, but you can't enable the private cloud service endpoint only. After cluster creation, you can't later change the service endpoints. | 
| strongSwan VPN service | See [strongSwan VPN service considerations](/docs/openshift?topic=openshift-vpn#strongswan_limitations). |
| Service IP addresses | You can have 65,000 IP addresses per cluster in the 172.21.0.0/16 range that you can assign to Kubernetes services within the cluster. |
| Subnets per VLAN | Each VLAN has a limit of 40 subnets. |
{: caption="Classic cluster networking limitations"}

### Storage
{: #classic_storage_limit}

Keep in mind that the [service](#tech_limits) limitations also apply.

| Category | Description |
| -------- | ----------- |
| Volume instances | You can have a total of 250 IBM Cloud infrastructure file and block storage volumes per account. If you mount more than this amount, you might see an "out of capacity" message when you provision persistent volumes. For more FAQs, see the [file](/docs/FileStorage?topic=FileStorage-file-storage-faqs#provision) and [block](/docs/BlockStorage?topic=BlockStorage-block-storage-faqs#authlimit) storage docs. If you want to mount more volumes, [contact IBM Support](/docs/get-support?topic=get-support-using-avatar). In your support ticket, include your account ID and the new file or block storage volume quota that you want.  |
| Portworx | Review the [Portworx limitations](/docs/openshift?topic=openshift-portworx#portworx_limitations). |
| File storage | Because of the way that {{site.data.keyword.cloud_notm}} NFS file storage configures Linux user permissions, you might encounter errors when you use file storage. If so, you might need to configure [{{site.data.keyword.redhat_openshift_notm}} Security Context Constraints](https://docs.openshift.com/container-platform/4.8/authentication/managing-security-context-constraints.html){: external} or use a different storage type. |
{: caption="Classic cluster storage limitations"}



## VPC cluster limitations
{: #ks_vpc_gen2_limits}

![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC clusters in {{site.data.keyword.openshiftlong_notm}} are released with the following limitations. Additionally, all the underlying [VPC quotas, VPC limits](/docs/vpc?topic=vpc-quotas), [VPC service limitations](/docs/vpc?topic=vpc-limitations), and [regular service limitations](#tech_limits) apply.
{: shortdesc}

### Compute
{: #vpc_gen2_compute_limit}

Keep in mind that the [service](#tech_limits) limitations also apply.

| Category | Description |
| -------- | ----------- |
| Encryption | The secondary disks of your worker nodes are encrypted at rest by default by the [underlying VPC infrastructure provider](/docs/vpc?topic=vpc-block-storage-about#vpc-storage-encryption). However, you can't [bring your own encryption to the underlying virtual server instances](/docs/vpc?topic=vpc-creating-instances-byok). |
| Location | VPC clusters are available only in [select multizone metro locations](/docs/openshift?topic=openshift-regions-and-zones#zones-vpc). |
| Versions | VPC clusters must run {{site.data.keyword.redhat_openshift_notm}} version 4. |
| Virtual Private Cloud | See [Limitations](/docs/vpc?topic=vpc-limitations) and [Quotas](/docs/vpc?topic=vpc-quotas). |
| v2 API | VPC clusters use the [{{site.data.keyword.openshiftlong_notm}} v2 API](/docs/openshift?topic=openshift-cs_api_install#api_about). The v2 API is currently under development, with only a limited number of API operations currently available. You can run certain v1 API operations against the VPC cluster, such as `GET /v1/clusters` or `ibmcloud oc cluster ls`, but not all the information that a Classic cluster has is returned or you might experience unexpected results. For supported VPC v2 operations, see the [CLI reference topic for VPC commands](/docs/containers?topic=containers-kubernetes-service-cli). |
| Worker node flavors | Only certain flavors are available for worker node [virtual machines](/docs/openshift?topic=openshift-planning_worker_nodes#vm). Bare metal machines are not supported.|
| Worker node host access | For security, you can't SSH into the worker node compute host. |
| Worker node updates | You can't update or reload worker nodes. Instead, you can delete the worker node and rebalance the worker pool with the `ibmcloud oc worker replace` command. If you replace multiple worker nodes at the same time, they are deleted and replaced concurrently, not one by one. Make sure that you have enough capacity in your cluster to reschedule your workloads before you replace worker nodes. |
{: caption="VPC cluster compute limitations"}


### Networking
{: #vpc_gen2_networking_limit}

Keep in mind that the [service](#tech_limits) limitations also apply.

| Category | Description |
| -------- | ----------- |
| App URL length | {{site.data.keyword.redhat_openshift_notm}} version 4.6 or later only: DNS resolution is managed by the cluster's [virtual private endpoint (VPE)](/docs/openshift?topic=openshift-vpc-subnets#vpc_basics_vpe), which can resolve URLs up to 130 characters. If you expose apps in your cluster with URLs, such as the Ingress subdomain or {{site.data.keyword.redhat_openshift_notm}} routes, ensure that the URLs are 130 characters or fewer. |
| Network speeds | [VPC profile network speeds](/docs/vpc?topic=vpc-profiles) refer to the speeds of the worker node interfaces. The maximum speed available to your worker nodes is `16Gbps`. Because IP in IP encapsulation is required for traffic between pods that are on different VPC worker nodes, data transfer speeds between pods on different worker nodes might be slower, about half the compute profile network speed. Overall network speeds for apps that you deploy to your cluster depend on the worker node size and application's architecture. |
| NodePort | You can access an app through a NodePort only if you are connected to your private VPC network, such as through a VPN connection. To access an app from the internet, you must use a VPC load balancer or Ingress service instead. |
| Pod network | VPC access control lists (ACLs) filter incoming and outgoing traffic for your cluster at the subnet level, and security groups filter incoming and outgoing traffic for your cluster at the worker nodes level. To control traffic within the cluster at the pod-to-pod level, you can't use VPC security groups or ACLs. Instead, use [Calico](/docs/containers?topic=containers-network_policies) and [Kubernetes network policies](/docs/containers?topic=containers-vpc-kube-policies), which can control the pod-level network traffic that uses IP in IP encapsulation. |
| Public gateway | If the public service endpoint is enabled, you must attach a public gateway to each VPC subnet so that your worker nodes can communicate on the public network. Default {{site.data.keyword.redhat_openshift_notm}} components, such as the web console and OperatorHub, require public network access.|
| Service endpoints | When you create your VPC cluster in the {{site.data.keyword.cloud_notm}} console, your cluster has both a public and a private cloud service endpoint. If you want only a private cloud service endpoint, you must create the cluster [in the CLI](/docs/openshift?topic=openshift-clusters#cluster_vpcg2_cli) instead, and include the `--disable-public-service-endpoint` flag. If you include this flag, your cluster is created with routers and Ingress controllers that expose your apps on the private network only by default. If you later want to expose apps to a public network, you must manually create public routers and Ingress controllers.|
| strongSwan VPN service | The strongSwan service is not supported. To connect your cluster to resources in an on-premises network or another VPC, see [Using VPN with your VPC](/docs/vpc?topic=vpc-vpn-onprem-example). |
| Subnets |  \n - See [VPC networking limitations](/docs/openshift?topic=openshift-vpc-subnets#vpc_basics_limitations). \n - Do not delete the subnets that you attach to your cluster during cluster creation or when you add worker nodes in a zone. If you delete a VPC subnet that your cluster used, any load balancers that use IP addresses from the subnet might experience issues, and you might be unable to create new load balancers.  |
| VPC load balancer | See [VPC load balancer limitations](/docs/openshift?topic=openshift-vpc-lbaas#lbaas_limitations). |
| VPC security groups | VPC clusters that run {{site.data.keyword.redhat_openshift_notm}} version 4.4 or earlier only: You must [allow inbound traffic requests to node ports on your worker nodes](/docs/openshift?topic=openshift-vpc-security-group). |
{: caption="VPC cluster networking limitations"}

### Storage
{: #vpc_gen2_storage_limit}

Keep in mind that the [service](#tech_limits) limitations also apply.

| Category | Description |
| -------- | ----------- |
| Storage class for profile sizes | The [available volume profiles](/docs/vpc?topic=vpc-block-storage-profiles) are limited to 2TB in size and 20,000 IOPS in capacity. |
| Supported types | You can set up {{site.data.keyword.cos_full_notm}} and {{site.data.keyword.databases-for}} only. |
| Unsupported types | NFS File Storage is not supported. |
| Volume attachments | See [Volume attachment limits](/docs/vpc?topic=vpc-attaching-block-storage#vol-attach-limits).|
| Portworx | Review the [Portworx limitations](/docs/openshift?topic=openshift-portworx#portworx_limitations). |
| {{site.data.keyword.block_storage_is_short}} | The default storage class in VPC clusters can not be changed. However, you can [create a custom storage class](/docs/openshift?topic=openshift-vpc-block#vpc-customize-storage-class). |
{: caption="VPC cluster storage limitations"}



## {{site.data.keyword.satelliteshort}} cluster limitations
{: #satellite_limits}

Review the following limitations for [{{site.data.keyword.openshiftlong_notm}} clusters that you create in a {{site.data.keyword.satelliteshort}} location](/docs/openshift?topic=openshift-satellite-clusters). Keep in mind that the [service](#tech_limits) limitations also apply.
{: shortdesc}

| Category | Description |
| -------- | ----------- |
| Cluster add-ons | Review the [unsupported managed add-ons for {{site.data.keyword.redhat_openshift_notm}} clusters](/docs/openshift?topic=openshift-managed-addons#addons-satellite) in a {{site.data.keyword.satelliteshort}} location. For example, the cluster autoscaler and Istio are not supported. |
| Key management service (KMS) | Cluster integration with a key management service (KMS) provider like {{site.data.keyword.keymanagementserviceshort}} is not supported.|
| Locations |  \n - {{site.data.keyword.redhat_openshift_notm}} clusters that are created in {{site.data.keyword.satelliteshort}} locations must use {{site.data.keyword.redhat_openshift_notm}} version 4.5 or later. \n - You must create your own [{{site.data.keyword.satelliteshort}} location](/docs/satellite?topic=satellite-locations) that is managed from [select {{site.data.keyword.cloud_notm}} multizone metros](/docs/satellite?topic=satellite-sat-regions).  |
| Logging and monitoring | You can't currently use the {{site.data.keyword.openshiftlong_notm}} console or the observability plug-in CLI (`ibmcloud ob`) to enable logging and monitoring for {{site.data.keyword.satelliteshort}} clusters. Instead, you can manually deploy [{{site.data.keyword.la_short}} agents](/docs/log-analysis?topic=log-analysis-tutorial-use-logdna) and [{{site.data.keyword.mon_short}} agents](/docs/monitoring?topic=monitoring-kubernetes_cluster#kubernetes_cluster) to your cluster to forward logs and metrics to {{site.data.keyword.la_full_notm}} and {{site.data.keyword.mon_full_notm}}. |
| Network |  \n - The private cloud service endpoint is not supported for {{site.data.keyword.satelliteshort}} clusters. \n - Your {{site.data.keyword.satelliteshort}} clusters can't use Kubernetes load balancers. \n - The hosts that run the worker nodes for your cluster must meet the [host networking](/docs/satellite?topic=satellite-reqs-host-network) and provider-specific requirements, such as for [AWS](/docs/satellite?topic=satellite-aws), [Azure](/docs/satellite?topic=satellite-azure), [GCP](/docs/satellite?topic=satellite-gcp), and [{{site.data.keyword.cloud_notm}}](/docs/satellite?topic=satellite-ibm) (testing and demonstration purposes only). |
| Storage for worker node hosts | See [Host storage and attached devices](/docs/satellite?topic=satellite-reqs-host-storage). |
| Storage for apps | No storage provider is installed in your {{site.data.keyword.satelliteshort}} clusters by default. Therefore, no pre-configured Kubernetes storage classes are set up by default in your clusters to store your application data in a Kubernetes persistent volume that is backed by storage device. For options to set up a storage provider, see [Understanding {{site.data.keyword.satelliteshort}} storage templates](/docs/satellite?topic=satellite-sat-storage-template-ov). |
| Worker nodes | Worker nodes run on hosts in your own infrastructure environments. The hosts must meet [host](/docs/satellite?topic=satellite-host-reqs) and provider-specific requirements, such as for [AWS](/docs/satellite?topic=satellite-aws), [Azure](/docs/satellite?topic=satellite-azure), [GCP](/docs/satellite?topic=satellite-gcp), and [{{site.data.keyword.cloud_notm}}](/docs/satellite?topic=satellite-ibm) (testing and demonstration purposes only). You are responsible for [managing the infrastructure lifecycle of your hosts](/docs/satellite?topic=satellite-host-concept), including adding and updating worker nodes. As such, worker node operations like `ibmcloud oc worker add, update, replace, reload` commands are not supported. |
| Worker pools | To use operations like `resize`, your worker pool uses [host labels](/docs/satellite?topic=satellite-assigning-hosts#host-autoassign-ov) that must match available (unassigned) hosts in the {{site.data.keyword.satelliteshort}} location. |
{: caption="{{site.data.keyword.satelliteshort}} cluster limitations"}







