---

copyright: 
  years: 2014, 2025
lastupdated: "2025-08-07"


keywords: openshift, http2, quota, app protocol, application protocol

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}




# Service limitations
{: #limitations}

{{site.data.keyword.openshiftlong}} and the {{site.data.keyword.redhat_openshift_notm}} open source project come with default service settings and limitations to ensure security, convenience, and basic functionality. Some limitations you might be able to change where noted.
{: shortdesc}


If you anticipate reaching any of the following {{site.data.keyword.openshiftlong_notm}} limitations, [contact IBM Support](/docs/account?topic=account-using-avatar) and provide the cluster ID, the new quota limit, and the region in your support ticket.
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
| Calico network plug-in | Changing the Calico plug-in, components, or default Calico settings is not supported. For example, don't deploy a new Calico plug-in version, or modify the daemon sets or deployments for the Calico components, default `IPPool` resources, or Calico nodes. Instead, you can follow the documentation to [create a Calico `NetworkPolicy` or `GlobalNetworkPolicy`](/docs/openshift?topic=openshift-network_policies), to [change the Calico MTU](/docs/openshift?topic=openshift-kernel#calico-mtu), or to [disable the port map plug-in for the Calico CNI](/docs/openshift?topic=openshift-kernel#calico-portmap). |
| Cluster quota | You can't exceed 100 clusters per region and per [infrastructure provider](/docs/openshift?topic=openshift-overview#what-compute-infra-is-offered). However, as of 01 January 2024, quotas are increased incrementally before reaching 100. If you need more of the resource, [contact IBM Support](/docs/account?topic=account-using-avatar). In the support case, include the new quota limit for the region and infrastructure provider that you want.. To list quotas, run `ibmcloud quota ls`. |
| Kubernetes | Make sure to review the [Kubernetes project limitations](https://kubernetes.io/docs/setup/best-practices/cluster-large/){: external}. |
| KMS provider | Customizing the IP addresses that are allowed to connect to your {{site.data.keyword.keymanagementservicefull}} instance is not supported.|
| {{site.data.keyword.redhat_openshift_notm}} | Make sure to review the [OpenShift Container Platform limitations](https://docs.redhat.com/documentation/openshift_container_platform/4.18/html/scalability_and_performance/planning-your-environment-according-to-object-maximums){: external} for your version.|
| Kubernetes pod logs | To check the logs for individual app pods, you can use the command line to run `oc logs <pod name>`. Do not use the Kubernetes dashboard to stream logs for your pods, which might cause a disruption in your access to the Kubernetes dashboard. |
| Monitoring |  - Because IBM manages your cluster master, event alerting for the master is disabled. IBM monitors your cluster master and fixes issues as they are detected. For this reason, in the Administrator perspective of the {{site.data.keyword.redhat_openshift_notm}}, you might see a `Not available` message for the control plane status. \n - The built-in Prometheus alert manager includes two rules that display as active alerts in a `FIRING` state: `KubeControllerManagerDown` and `KubeSchedulerDown`. These components are part of the IBM-managed cluster master, so you can ignore these alerts. |
| Operating system | Worker nodes must run one of the supported operating systems. You can't create a cluster with worker nodes that run different types of operating systems. For more information, see the [{{site.data.keyword.openshiftshort}} version information](/docs/openshift?topic=openshift-openshift_versions). |
| OperatorHub catalog | To use the OperatorHub catalog in private clusters see [Disabling OperatorHub and mirroring catalog source images to `icr.io`](/docs/openshift?topic=openshift-operators#mirror-operatorhub). |
| Pod instances | You can run 110 pods per worker node. If you have worker nodes with 11 CPU cores or more, you can support 10 pods per core, up to a limit of 250 pods per worker node. The number of pods includes `kube-system` and `ibm-system` pods that run on the worker node. For improved performance, consider limiting the number of pods that you run per compute core so that you don't overuse the worker node. For example, on a worker node with a `b3c.4x16` flavor, you might run 10 pods per core that use no more than 75% of the worker node total capacity. |
| [Deprecated]{: tag-red} Time-based one-time passcode (TOTP) | To use [TOTP](/docs/account?topic=account-legacy-mfa#account-based), make sure that you [enable multifactor authentication (MFA)](/docs/account?topic=account-enablemfa) for your entire {{site.data.keyword.cloud_notm}} account. If MFA is enabled only for some users but not at the account level, authentication errors might occur.  |
| Worker node quota | A maximum 500 worker nodes for any accounts created before 01 January 2024. For accounts created on or after that date, the maximum quota is 200 after a period of lower quotas. Quotas apply per cluster [infrastructure provider](/docs/openshift?topic=openshift-overview#what-compute-infra-is-offered). If you need more of the resource, [contact IBM Support](/docs/account?topic=account-using-avatar). In the support case, include the new quota limit for the region and infrastructure provider that you want.. To list quotas run, `ibmcloud ks quota ls`. |
| Worker pool size | You must always have a minimum of 2 nodes in your cluster. Because of the worker node quota, you are limited in the number of worker pools per cluster and number of worker nodes per worker pool. For example, with the default worker node quota of 500 per region, you might have up to 500 worker pools of 1 worker node each in a region with only 1 cluster. Or, you might have 1 worker pool with up to 500 worker nodes in a region with only 1 cluster. |
| Red Hat Enterprise Linux CoreOS worker nodes | The maximum amount of zones added to a cluster is 15. For example, 4 RHCOS worker pools with 3 zones each will account for 12/15 of the quota for that cluster. |
| Number of worker nodes | Clusters can have a maximum of 500 worker nodes. |
| Red Hat Enterprise Linux CoreOS worker nodes | The maximum amount of zones added to a cluster is 15. For example, 4 RHCOS worker pools with 3 zones each will account for 12/15 of the quota for that cluster. |
| Cluster naming | To ensure that the Ingress subdomain and certificate are correctly registered, the first 24 characters of the clusters' names must be different. If you create and delete clusters with the same name or names that have the same first 24 characters 5 times or more within 7 days, such as for automation or testing purposes, you might reach the [Let's Encrypt Duplicate Certificate rate limit](/docs/openshift?topic=openshift-cs_rate_limit). |
| Resource groups | A cluster can be created in only one resource group that you can't change afterward. If you create a cluster in the wrong resource group, you must delete the cluster and re-create it in the correct resource group. Furthermore, if you need to use the `ibmcloud oc cluster service bind` command to [integrate with an {{site.data.keyword.cloud_notm}} service](/docs/openshift?topic=openshift-service-binding#bind-services), that service must be in the same resource group as the cluster. Services that don't use resource groups like {{site.data.keyword.registrylong_notm}} or that don't need service binding like {{site.data.keyword.logs_full_notm}} work even if the cluster is in a different resource group. |
{: caption="{{site.data.keyword.openshiftlong_notm}} limitations"}





### {{site.data.keyword.openshiftlong_notm}} cluster limitations
{: #ocp4_limitations}

Review limitations that are specific to {{site.data.keyword.redhat_openshift_notm}} clusters. Keep in mind that the [service](#tech_limits) and [classic cluster](#classic_limits) or [VPC cluster](#ks_vpc_gen2_limits) limitations also apply.
{: shortdesc}

| Category | Description |
| -------- | ----------- |
| Cluster autoscaling | The {{site.data.keyword.redhat_openshift_notm}} cluster autoscaler from the {{site.data.keyword.redhat_openshift_notm}} **Administration > Cluster Settings** console or `ClusterAutoscaler` object from the `autoscaling.openshift.io/v1` API is not supported. Instead, use the [`ibm-iks-cluster-autoscaler` Helm plug-in](/docs/openshift?topic=openshift-cluster-scaling-install-addon). |
| Cluster updates | You must [update your cluster](/docs/openshift?topic=openshift-update) by using the {{site.data.keyword.openshiftlong_notm}} API, CLI, or console tools. You can't update your cluster version from OpenShift Container Platform tools such as the {{site.data.keyword.redhat_openshift_notm}} web console. |
| Container logs | If you use a container logging operator such as Fluentd to send logs to an ElasticSearch stack, you must [update the cluster logging deployment to use the `ibmc-block-gold` storage class](/docs/openshift?topic=openshift-health#oc_logging_operator). |
| Private clusters | Depending on the infrastructure provider, your options for private clusters are limited. \n - **VPC**: When you create your VPC cluster in the {{site.data.keyword.cloud_notm}} console, your cluster has both a public and a private cloud service endpoint. If you want only a private cloud service endpoint, you must create the cluster [in the CLI](/docs/openshift?topic=openshift-cluster-create-vpc-gen2&interface=cli) instead, and include the `--disable-public-service-endpoint` option. If you include this option, your cluster is created with routers and Ingress controllers that expose your apps on the private network only by default. If you later want to expose apps to a public network, you must manually create public routers and Ingress controllers. \n - **Classic**: You can enable the public and private cloud service endpoint or the public cloud service endpoint only, but you can't enable the private cloud service endpoint only. After cluster creation, you can't later change the service endpoints.  |
| Logging | To set up an [OpenShift Container Platform Elasticsearch, Fluentd, and Kibana (EFK) stack](https://docs.redhat.com/documentation/openshift_container_platform/4.18/html/logging/logging-6-1){: external}, see [installing the cluster logging operator](/docs/openshift?topic=openshift-health#oc_logging_operator).|
| Service catalog | The service catalog is not supported. Use [Operators](/docs/openshift?topic=openshift-operators#operators_4) instead. Do not use the OperatorHub to install the service catalog. |
| Service mesh | The Istio managed add-on is not supported. Instead, use the [Red Hat service mesh operator](https://docs.redhat.com/documentation/openshift_container_platform/4.18/html/service_mesh/service-mesh-1-x){: external}. **Note**: The default {{site.data.keyword.cloud_notm}} configuration of the routers enables host networking, which is not compatible with the service mesh network policy. For the service mesh ingress to work, [apply a network policy](https://gist.githubusercontent.com/kitch/39c504a2ed9e381c2aadea436d5b52e4/raw/d8efa69f41d41425b16bb363a881a98d40d3708c/mesh-policy.yaml){: external}.|
{: caption="OpenShift Container Platform cluster limitations"}




## Classic cluster limitations
{: #classic_limits}

Classic infrastructure clusters in {{site.data.keyword.openshiftlong_notm}} are released with the following limitations.
{: shortdesc}

### Compute
{: #classic_compute_limit}

Keep in mind that the [service](#tech_limits) limitations also apply.

| Category | Description |
| -------- | ----------- |
| Reserved instances | [Reserved capacity and reserved instances](/docs/virtual-servers?topic=virtual-servers-provisioning-reserved-capacity-and-instances) are not supported. |
| Worker node flavors | Worker nodes are available in select flavors of compute resources. |
| Worker node host access | For security, you can't SSH into the worker node compute host. |
{: caption="Classic cluster compute limitations"}

### Networking
{: #classic_networking_limit}

Keep in mind that the [service](#tech_limits) limitations also apply.

| Category | Description |
| -------- | ----------- |
| Ingress ALBs |  \n - The Ingress application load balancer (ALB) can process 32,768 connections per second. If your Ingress traffic exceeds this number,  [scale up the number of ALB replicas](/docs/containers?topic=containers-comm-ingress-annotations) in your cluster to handle the increased workload. \n - ALBs that run the [{{site.data.keyword.openshiftlong_notm}} custom Ingress image](/docs/containers?topic=containers-managed-ingress-about) only: HTTP/2 is not supported. \n - ALBs that run the [{{site.data.keyword.openshiftlong_notm}} custom Ingress image] (/docs/containers?topic=containers-managed-ingress-about) only: The names of the `ClusterIP` services that expose your apps must be unique across all namespaces in your cluster.  |
| Network load balancers (NLB)| - You can't create version 2.0 network load balancers (NLB 2.0) to expose your apps. \n - You can't create subdomains for private NLBs. \n - You can register up to 128 subdomains. This limit can be lifted on request by opening a [support case](/docs/account?topic=account-using-avatar).  | 
| {{site.data.keyword.redhat_openshift_notm}} web console | The web console cannot be exposed on the private network on clusters that have both public and private endpoints. If you want to expose the web console on the private network, your cluster cannot have a public endpoint enabled.  | 
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
| Volume instances | You can have a total of 250 IBM Cloud infrastructure file and block storage volumes per account. If you mount more than this amount, you might see an `out of capacity` message when you provision persistent volumes. For more FAQ, see the [file](/docs/FileStorage?topic=FileStorage-file-storage-faqs#provision) and [block](/docs/BlockStorage?topic=BlockStorage-block-storage-faqs#authlimit) storage docs. If you want to mount more volumes, [contact IBM Support](/docs/account?topic=account-using-avatar). In your support ticket, include your account ID and the new file or block storage volume quota that you want.  |
| Portworx | Review the [Portworx limitations](/docs/openshift?topic=openshift-storage_portworx_plan#portworx_limitations). |
| File storage | Because of the way that {{site.data.keyword.cloud_notm}} NFS file storage configures Linux user permissions, you might encounter errors when you use file storage. If so, you might need to configure [{{site.data.keyword.redhat_openshift_notm}} Security Context Constraints](https://docs.redhat.com/documentation/openshift_container_platform/4.18/html/authentication_and_authorization/managing-pod-security-policies){: external} or use a different storage type. |
{: caption="Classic cluster storage limitations"}

## Classic user access
{: #classic_access_limit}

Keep in mind that the [service](#tech_limits) limitations also apply.

| Category | Description |
| -------- | ----------- |
| IP address access | Restricting access for specific users by enabling IP address access is not supported by {{site.data.keyword.openshiftlong_notm}}. If you want to restrict user access or restrict which services and VPCs a user can access, consider [context-based restriction](/docs/openshift?topic=openshift-cbr-tutorial).  |
{: caption="Classic cluster user access limitations"}



## VPC cluster limitations
{: #ks_vpc_gen2_limits}

VPC clusters in {{site.data.keyword.openshiftlong_notm}} are released with the following limitations. Additionally, all the underlying [VPC quotas, VPC limits](/docs/vpc?topic=vpc-quotas), [VPC service limitations](/docs/vpc?topic=vpc-limitations), and [regular service limitations](#tech_limits) apply.
{: shortdesc}

### Compute
{: #vpc_gen2_compute_limit}

Keep in mind that the [service](#tech_limits) limitations also apply.

| Category | Description |
| -------- | ----------- |
| Clusters per VPC | VPCs are limited to 25 clusters each. |
| Encryption | The secondary disks of your worker nodes are encrypted at rest by default by the [underlying VPC infrastructure provider](/docs/vpc?topic=vpc-block-storage-about#vpc-storage-encryption). However, you can't [bring your own encryption to the underlying virtual server instances](/docs/vpc?topic=vpc-file-storage-byok-encryption&interface=ui). |
| Location | VPC clusters are available only in [select multizone regions](/docs/openshift?topic=openshift-regions-and-zones#zones-vpc). |
| Virtual Private Cloud | See [Limitations](/docs/vpc?topic=vpc-limitations) and [Quotas](/docs/vpc?topic=vpc-quotas). |
| Worker node flavors | Only certain flavors are available for worker node virtual machines. Bare metal machines are not supported.|
| Worker node host access | For security, you can't SSH into the worker node compute host. |
| Worker node updates | You can't update or reload VPC worker nodes. Instead, you can delete the worker node and rebalance the worker pool with the `ibmcloud oc worker replace` command. If you replace multiple worker nodes at the same time, they are deleted and replaced concurrently, not one by one. Make sure that you have enough capacity in your cluster to reschedule your workloads before you replace worker nodes. |
{: caption="VPC cluster compute limitations"}


### Networking
{: #vpc_gen2_networking_limit}

Keep in mind that the [service](#tech_limits) limitations also apply.

| Category | Description |
| -------- | ----------- |
| App URL length | DNS resolution is managed by the cluster's [virtual private endpoint (VPE)](/docs/openshift?topic=openshift-vpc-subnets#vpc_basics_vpe), which can resolve URLs up to 130 characters. If you expose apps in your cluster with URLs, such as the Ingress subdomain or {{site.data.keyword.redhat_openshift_notm}} routes, ensure that the URLs are 130 characters or fewer. |
| Network speeds | [VPC profile network speeds](/docs/vpc?topic=vpc-profiles) refer to the speeds of the worker node interfaces. The bandwidth available for VPC instances is shared between storage and network traffic. By default, the storage allocation is 25% of maximum bandwidth. Network speed, as shown in the tables below, is the network bandwidth available to a worker with a single network interface after deducting the default 25% storage bandwidth allocation. |
| NodePort | You can access an app through a NodePort only if you are connected to your private VPC network, such as through a VPN connection. To access an app from the internet, you must use a VPC load balancer or Ingress service instead. |
| Pod network | VPC access control lists (ACLs) filter incoming and outgoing traffic for your cluster at the subnet level, and security groups filter incoming and outgoing traffic for your cluster at the worker nodes level. To control traffic within the cluster at the pod-to-pod level, you can't use VPC security groups or ACLs. Instead, use [Calico](/docs/openshift?topic=openshift-network_policies) and [Kubernetes network policies](/docs/openshift?topic=openshift-vpc-kube-policies), which can control the pod-level network traffic that uses IP in IP encapsulation. |
| Public gateway | If the public service endpoint is enabled, you must attach a public gateway to each VPC subnet so that your worker nodes can communicate on the public network. Default {{site.data.keyword.redhat_openshift_notm}} components, such as the web console and OperatorHub, require public network access.|
| Service endpoints | When you create your VPC cluster in the {{site.data.keyword.cloud_notm}} console, your cluster has both a public and a private cloud service endpoint. If you want only a private cloud service endpoint, you must create the cluster [in the CLI](/docs/openshift?topic=openshift-cluster-create-vpc-gen2&interface=cli) instead, and include the `--disable-public-service-endpoint` option. If you include this option, your cluster is created with routers and Ingress controllers that expose your apps on the private network only by default. If you later want to expose apps to a public network, you must manually create public routers and Ingress controllers.|
| strongSwan VPN service | The strongSwan service is not supported. To connect your cluster to resources in an on-premises network or another VPC, see [Using VPN with your VPC](/docs/vpc?topic=vpc-vpn-onprem-example). |
| Subnets |  \n - See [VPC networking limitations](/docs/openshift?topic=openshift-vpc-subnets#vpc_basics_limitations). \n - Do not delete the subnets that you attach to your cluster during cluster creation or when you add worker nodes in a zone. If you delete a VPC subnet that your cluster used, any load balancers that use IP addresses from the subnet might experience issues, and you might be unable to create new load balancers.  |
| VPC load balancer | See [VPC load balancer limitations](/docs/openshift?topic=openshift-vpclb-about#vpclb_limit). |
{: caption="VPC cluster networking limitations"}

### Storage
{: #vpc_gen2_storage_limit}

Keep in mind that the [service](#tech_limits) limitations also apply.

| Category | Description |
| -------- | ----------- |
| Storage class for profile sizes | For more information, see [available volume profiles](/docs/vpc?topic=vpc-block-storage-profiles). |
| Supported types | You can set up {{site.data.keyword.cos_full_notm}} and {{site.data.keyword.databases-for}} only. |
| Volume attachments | See [Volume attachment limits](/docs/vpc?topic=vpc-attaching-block-storage#vol-attach-limits).|
| Portworx | Review the [Portworx limitations](/docs/openshift?topic=openshift-storage_portworx_plan#portworx_limitations). |
| {{site.data.keyword.block_storage_is_short}} | The default storage class in VPC clusters cannot be changed. However, you can [create your own storage class](/docs/openshift?topic=openshift-vpc-block#vpc-customize-storage-class). |
{: caption="VPC cluster storage limitations"}

## VPC user access
{: #vpc_access_limit}

Keep in mind that the [service](#tech_limits) limitations also apply.

| Category | Description |
| -------- | ----------- |
| IP address access | Restricting access for specific users by enabling IP address access is not supported by {{site.data.keyword.openshiftlong_notm}}. If you want to restrict user access or restrict which services and VPCs a user can access, consider [context-based restriction](/docs/openshift?topic=openshift-cbr-tutorial).  |
{: caption="VPC cluster user access limitations"}



## {{site.data.keyword.satelliteshort}} cluster limitations
{: #satellite_limits}

Review the following limitations for [{{site.data.keyword.openshiftlong_notm}} clusters that you create in a {{site.data.keyword.satelliteshort}} location](/docs/openshift?topic=openshift-satellite-clusters). Keep in mind that the [service](#tech_limits) limitations also apply.
{: shortdesc}

| Category | Description |
| -------- | ----------- |
| Cluster add-ons | Review the [unsupported managed add-ons for {{site.data.keyword.redhat_openshift_notm}} clusters](/docs/openshift?topic=openshift-managed-addons#addons-satellite) in a {{site.data.keyword.satelliteshort}} location. For example, the cluster autoscaler and Istio are not supported. |
| Network |  \n - By default, there is no load balancer controller deployed with {{site.data.keyword.satelliteshort}} clusters and therefore, [Kubernetes LoadBalancer services](https://kubernetes.io/docs/tasks/access-application-cluster/create-external-load-balancer/){: external} are not provision by default. You can integrate your own load balancer solution into clusters, such as [MetalLB](/docs/openshift?topic=openshift-sat-expose-apps#sat-expose-metallb). \n - The hosts that run the worker nodes for your cluster must meet the [host networking](/docs/satellite?topic=satellite-reqs-host-network) and provider-specific requirements, such as for [AWS](/docs/satellite?topic=satellite-aws), [Azure](/docs/satellite?topic=satellite-azure), [GCP](/docs/satellite?topic=satellite-gcp), and [{{site.data.keyword.cloud_notm}}](/docs/satellite?topic=satellite-ibm) (testing and demonstration purposes only). \n - Because VXLAN encapsulation is required for traffic between pods that are on different worker nodes, data transfer speeds between pods on different worker nodes might be slower than the network capability of the hosts. |
| Storage for worker node hosts | See [Host storage and attached devices](/docs/satellite?topic=satellite-reqs-host-storage). |
| Storage for apps | No storage provider is installed in your {{site.data.keyword.satelliteshort}} clusters by default. Therefore, no pre-configured Kubernetes storage classes are set up by default in your clusters to store your application data in a Kubernetes persistent volume that is backed by storage device. For options to set up a storage provider, see [Understanding {{site.data.keyword.satelliteshort}} storage templates](/docs/satellite?topic=satellite-storage-template-ov). |
| Worker nodes | Worker nodes run on hosts in your own infrastructure environments. The hosts must meet [host](/docs/satellite?topic=satellite-host-reqs) and provider-specific requirements, such as for [AWS](/docs/satellite?topic=satellite-aws), [Azure](/docs/satellite?topic=satellite-azure), [GCP](/docs/satellite?topic=satellite-gcp), and [{{site.data.keyword.cloud_notm}}](/docs/satellite?topic=satellite-ibm) (testing and demonstration purposes only). You are responsible for [managing the infrastructure lifecycle of your hosts](/docs/satellite?topic=satellite-host-update-location), including adding and [updating worker nodes](/docs/satellite?topic=satellite-host-update-workers). As such, worker node operations like `ibmcloud oc worker add, update, replace, reload` commands are not supported. |
| Worker pools | To use operations like `resize`, your worker pool uses [host labels](/docs/satellite?topic=satellite-host-autoassign-ov) that must match available (unassigned) hosts in the {{site.data.keyword.satelliteshort}} location. |
| Single node clusters | Any cluster with fewer than three worker nodes lacks high availability. By provisioning a single-node cluster, you accept that you are more likely to experience downtime and disruptions in your workload, and that regular worker node upgrades result in your workload going offline. Additionally, if a cluster is provisioned as a single-node cluster, it cannot later be converted to a standard, highly available cluster. You can add more nodes, but standard deployments do not increase in replica size and the cluster does not become highly available. Single node clusters must run on a {{site.data.keyword.satelliteshort}} location with [Red Hat CoreOS (RHCOS) enabled](/docs/satellite?topic=satellite-locations#verify-coreos-location). Control plane hosts on your location and the host you assign to your single-node cluster must run either the RHEL 8 or RHCOS operating systems. Only supported for {{site.data.keyword.satelliteshort}} clusters that run version 4.11 or later. OpenShift Data Foundation is not supported on single-node clusters. Portworx is not supported on single-node clusters.
{: caption="{{site.data.keyword.satelliteshort}} cluster limitations"}


## Unsupported features and operators in {{site.data.keyword.openshiftlong_notm}}
{: #not-supported-features-table}

The following features and operators are not supported in {{site.data.keyword.openshiftlong_notm}}.

Instead of tuning worker node performance with `MachineConfig` files in {{site.data.keyword.redhat_openshift_notm}}, you can modify the host with a `daemonset` file. For more information, see [Changing the Calico MTU](/docs/openshift?topic=openshift-kernel#calico-mtu) or [Tuning performance for Red Hat CoreOS worker nodes](/docs/openshift?topic=openshift-rhcos-performance).
{: note}

* AMQ Broker
* AMQ Broker LTS
* AMQ Interconnect
* AMQ Online
* AMQ Streams
* Ansible Automation Platform Resource Operator
* API Designer
* Business Automation Operator
* Camel K
* Cost management Operator
* Data Grid Operator
* Device Manager
* File Integrity Operator
* Fuse Console
* Fuse Online
* Gatekeeper Operator
* JBoss EAP
* JBoss Web Server
* Logical volume manager storage (LVM)
* MachineConfigs
* Metering and Cost Management SaaS Service
* OpenShift Cloud Manager (OCM) SaaS Service
* OpenShift Cluster-Wide Proxy
* OpenShift Data Foundation: Supported through the [cluster add-on](/docs/openshift?topic=openshift-ocs-storage-prep) for Classic and VPC clusters or through the {{site.data.keyword.satelliteshort}} [template](/docs/satellite?topic=satellite-storage-template-ov) for {{site.data.keyword.satelliteshort}} clusters.
* OpenShift Virtualization Operator
* OVS and OVN SDN
* Performance Add-on Operator
* PTP Operator
* Quay Operator
* Red Hat OpenStack Platform `Kuryr` Integration
* Red Hat Integration Operator
* Service Registry Operator
* Smart Gateway Operator
* SR-IOV Network Operator: Supported in {{site.data.keyword.satelliteshort}} clusters only.
* Telemeter and Insights Connected Experience
* Windows Machine Config: Worker nodes with Windows operating systems are not supported.
* `ImageContentSourcePolicy`, `ImageDigestMirrorSet`, and `ImageTagMirrorSet` are not supported.
