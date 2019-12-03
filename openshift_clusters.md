---

copyright:
  years: 2014, 2019
lastupdated: "2019-12-03"

keywords: openshift, roks, rhoks, rhos, clusters

subcollection: openshift

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:download: .download}
{:preview: .preview} 

# Creating OpenShift clusters
{: #clusters}

Create a cluster in {{site.data.keyword.openshiftlong}}.
{: shortdesc}


After [getting started](/docs/containers?topic=containers-getting-started), you might want to create a cluster that is customized to your use case and different public and private cloud environments. Consider the following steps to create the right cluster each time.

1.  [Prepare your account to create clusters](/docs/openshift?topic=openshift-clusters#cluster_prepare). This step includes creating a billable account, setting up an API key with infrastructure permissions, making sure that you have Administrator access in {{site.data.keyword.cloud_notm}} IAM, planning resource groups, and setting up account networking.
2.  [Decide on your cluster setup](/docs/openshift?topic=openshift-clusters#prepare_cluster_level). This step includes planning cluster network and HA setup, estimating costs, and if applicable, allowing network traffic through a firewall.
3.  Create your <ff-roks311-vpc>[VPC](#clusters_vpc_standard) or [classic](#clusters_standard) cluster</ff-roks311-vpc>[cluster](#clusters_standard) by following the steps in the {{site.data.keyword.cloud_notm}} console or CLI.

<br />


## Sample commands
{: #cluster_create_samples}

Have you created a cluster before and are just looking for quick example commands? Try these examples.
{: shortdesc}



<ff-roks311-vpc>**Classic clusters**:</ff-roks311-vpc>
* Classic cluster, shared virtual machine:
   ```
   ibmcloud oc cluster create classic --name my_cluster --kube-version 3.11_openshift --zone dal10 --machine-type b3c.4x16 --hardware shared --workers 3 --public-vlan <public_VLAN_ID> --private-vlan <private_VLAN_ID>
   ```
   {: pre}
*  Classic cluster, bare metal:
   ```
   ibmcloud oc cluster create classic --name my_cluster --kube-version 3.11_openshift --zone dal10 --machine-type mb2c.4x32 --hardware dedicated --workers 3 --public-vlan <public_VLAN_ID> --private-vlan <private_VLAN_ID>
   ```
   {: pre}
*  For a classic multizone cluster, after you created the cluster in a [multizone metro](/docs/openshift?topic=openshift-regions-and-zones#zones), [add zones](/docs/openshift?topic=openshift-add_workers#add_zone):
   ```
   ibmcloud oc zone add classic --zone <zone> --cluster <cluster_name_or_ID> --worker-pool <pool_name> --private-vlan <private_VLAN_ID> --public-vlan <public_VLAN_ID>
   ```
   {: pre}

<ff-roks311-vpc>

**VPC clusters**:
*  VPC Gen 1 compute cluster:
   ```
   ibmcloud oc cluster create vpc-classic --name my_cluster --kube-version 3.11_openshift --zone us-east-1 --vpc-id <VPC_ID> --subnet-id <VPC_SUBNET_ID> --flavor b2.4x16 --workers 3
   ```
   {: pre}
*  For a VPC multizone cluster, after you created the cluster in a [multizone metro](/docs/openshift?topic=openshift-regions-and-zones#zones), [add zones](/docs/openshift?topic=openshift-add_workers#add_zone):
   ```
   ibmcloud oc zone add vpc-classic --zone <zone> --cluster <cluster_name_or_ID> --worker-pool <pool_name> --subnet-id <VPC_SUBNET_ID>
   ```
   {: pre}
</ff-roks311-vpc>

<br />



## Prepare to create clusters at the account level
{: #cluster_prepare}

Prepare your {{site.data.keyword.cloud_notm}} account for {{site.data.keyword.containerlong_notm}}. After the account administrator makes these preparations, you might not need to change them each time that you create a cluster. However, each time that you create a cluster, you still want to verify that the current account-level state is what you need it to be.
{: shortdesc}

1. [Create or upgrade your account to a billable account ({{site.data.keyword.cloud_notm}} Pay-As-You-Go or Subscription)](https://cloud.ibm.com/registration/).

2. [Set up an API key for Red Hat OpenShift on IBM Cloud](/docs/openshift?topic=openshift-users#api_key) in the region and resource groups that you want to create clusters. Assign the API key with the appropriate service and infrastructure permissions to create clusters.<p class="tip">Are you the account owner? You already have the necessary permissions! When you create a cluster, the API key for that region and resource group is set with your credentials.</p>

    **Services**:
    * [**Administrator** platform role](/docs/openshift?topic=openshift-users#platform) for {{site.data.keyword.containerlong_notm}} at the account level.
    * [**Writer** or **Manager** service role](/docs/openshift?topic=openshift-users#platform) for {{site.data.keyword.containerlong_notm}}.
    * [**Administrator** platform role](/docs/openshift?topic=openshift-users#platform) for Container Registry at the account level. If your account predates 4 October 2018, you need to [enable {{site.data.keyword.cloud_notm}} IAM policies for {{site.data.keyword.registryshort_notm}}](/docs/services/Registry?topic=registry-user#existing_users). With IAM policies, you can control access to resources such as registry namespaces.

    **Infrastructure**:
    * <ff-roks311-vpc>Classic clusters only: </ff-roks311-vpc>**Super User** role or the [minimum required permissions](/docs/openshift?topic=openshift-access_reference#infra) for classic infrastructure.<ff-roks311-vpc>
    * VPC clusters only: [**Administrator** platform role for VPC Infrastructure](/docs/vpc-on-classic?topic=vpc-on-classic-managing-user-permissions-for-vpc-resources).</ff-roks311-vpc>

3. Verify that you as a user (not just the API key) have the **Administrator** platform role for {{site.data.keyword.containerlong_notm}}. To allow your cluster to pull images from the private registry, you also need the **Administrator** platform role for {{site.data.keyword.registrylong_notm}}. If you are the account owner, you already have these permissions.
  1. From the [{{site.data.keyword.cloud_notm}} console ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/) menu bar, click **Manage > Access (IAM)**.
  2. Click the **Users** page, and then from the table, select yourself.
  3. From the **Access policies** tab, confirm that your **Role** is **Administrator**. You can be the **Administrator** for all the resources in the account, or at least for {{site.data.keyword.containerlong_notm}}. **Note**: If you have the **Administrator** role for {{site.data.keyword.containerlong_notm}} in only one resource group or region instead of the entire account, you must have at least the **Viewer** role at the account level to see the account's VLANs.
  <p class="tip">Make sure that your account administrator does not assign you the **Administrator** platform role at the same time as scoping the access policy to a namespace.</p>

4. If your account uses multiple resource groups, figure out your account's strategy for [managing resource groups](/docs/openshift?topic=openshift-users#resource_groups).
  * The cluster is created in the resource group that you target when you log in to {{site.data.keyword.cloud_notm}}. If you do not target a resource group, the default resource group is automatically targeted. Free clusters are created in the `default` resource group.
  * If you want to create a cluster in a different resource group than the default, you need at least the **Viewer** role for the resource group. If you do not have any role for the resource group, your cluster is created in the default resource group.
  * You cannot change a cluster's resource group. Furthermore, if you need to use the `ibmcloud oc cluster service bind` [command](/docs/containers-cli-plugin?topic=containers-cli-plugin-kubernetes-service-cli#cs_cluster_service_bind) to [integrate with an {{site.data.keyword.cloud_notm}} service](/docs/containers?topic=containers-service-binding#bind-services), that service must be in the same resource group as the cluster. Services that do not use resource groups like {{site.data.keyword.registrylong_notm}} or that do not need service binding like {{site.data.keyword.la_full_notm}} work even if the cluster is in a different resource group.
  * Consider giving clusters unique names across resource groups and regions in your account to avoid naming conflicts. You cannot rename a cluster.

5. Plan your cluster network setup so that your cluster meets the needs of your workloads and environment. Then, set up your IBM Cloud infrastructure networking to allow worker-to-master and user-to-master communication. Your cluster network setup varies with the infrastructure provider that you choose (classic or VPC). For more information, see [Planning your cluster network setup](/docs/openshift?topic=openshift-plan_clusters).<ff-roks311-vpc>
  * **VPC clusters only**: Your VPC clusters are created with a public and a private service endpoint by default.
    1. [Enable your {{site.data.keyword.cloud_notm}} account to use service endpoints](/docs/account?topic=account-vrf-service-endpoint#service-endpoint).
    2. Optional: If you want your VPC clusters to communicate with classic clusters over the private network interface, you can choose to set up classic infrastructure access from the VPC that your cluster is in. Note that you can set up classic infrastructure access for only one VPC per region and [Virtual Routing and Forwarding (VRF)](/docs/resources?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud) is required in your {{site.data.keyword.cloud_notm}} account. For more information, see [Setting up access to your Classic Infrastructure from VPC](/docs/vpc-on-classic?topic=vpc-on-classic-setting-up-access-to-your-classic-infrastructure-from-vpc).</ff-roks311-vpc>

  * **Classic clusters only, VRF and service endpoint enabled accounts**: You must set up your account to use VRF and service endpoints to support scenarios such as running internet-facing workloads and extending your on-premises data center. After you set up the account, your VPC and classic clusters are created with a public and a private service endpoint by default.
    1. Enable [VRF](/docs/resources?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud) in your IBM Cloud infrastructure account. To check whether a VRF is already enabled, use the `ibmcloud account show` command.
    2. [Enable your {{site.data.keyword.cloud_notm}} account to use service endpoints](/docs/account?topic=account-vrf-service-endpoint#service-endpoint).
    3. **Optional, private service endpoint only**: Set up connectivity to the private network. The OpenShift master is accessible through the private service endpoint if authorized cluster users are in your {{site.data.keyword.cloud_notm}} private network or are connected to the private network through a [VPN connection](/docs/infrastructure/iaas-vpn?topic=VPN-getting-started) or [{{site.data.keyword.cloud_notm}} Direct Link](/docs/infrastructure/direct-link?topic=direct-link-get-started-with-ibm-cloud-direct-link). However, communication with the Kubernetes master over the private service endpoint must go through the <code>166.X.X.X</code> IP address range, which is not routable from a VPN connection or through {{site.data.keyword.cloud_notm}} Direct Link. You can expose the private service endpoint of the master for your cluster users by using a private network load balancer (NLB). The private NLB exposes the private service endpoint of the master as an internal <code>10.X.X.X</code> IP address range that users can access with the VPN or {{site.data.keyword.cloud_notm}} Direct Link connection. If you enable only the private service endpoint, you can use the Kubernetes dashboard or temporarily enable the public service endpoint to create the private NLB. For more information, see [Accessing clusters through the private service endpoint](/docs/openshift?topic=openshift-access_cluster#access_private_se).

  * **Classic clusters only, non-VRF and non-service endpoint accounts**: If you do not set up your account to use VRF and service endpoints, you can create only classic clusters that use VLAN spanning to communicate with each other on the public and private network.
    * To use the public service endpoint only (run internet-facing workloads):
      1. Enable [VLAN spanning](/docs/infrastructure/vlans?topic=vlans-vlan-spanning#vlan-spanning) for your IBM Cloud infrastructure account so that your worker nodes can communicate with each other on the private network. To perform this action, you need the **Network > Manage Network VLAN Spanning** [infrastructure permission](/docs/openshift?topic=openshift-users#infra_access), or you can request the account owner to enable it. To check whether VLAN spanning is already enabled, use the `ibmcloud oc vlan spanning get --region <region>` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_vlan_spanning_get).
    * To use a gateway appliance (extend your on-premises data center):
      1. Enable [VLAN spanning](/docs/infrastructure/vlans?topic=vlans-vlan-spanning#vlan-spanning) for your IBM Cloud infrastructure account so that your worker nodes can communicate with each other on the private network. To perform this action, you need the **Network > Manage Network VLAN Spanning** [infrastructure permission](/docs/openshift?topic=openshift-users#infra_access), or you can request the account owner to enable it. To check whether VLAN spanning is already enabled, use the `ibmcloud oc vlan spanning get --region <region>` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_vlan_spanning_get).
      2. Configure a gateway appliance to connect your cluster to the on-premises network. For example, you might choose to set up a [Virtual Router Appliance](/docs/infrastructure/virtual-router-appliance?topic=virtual-router-appliance-about-the-vra) or a [Fortigate Security Appliance](/docs/services/vmwaresolutions/services?topic=vmware-solutions-fsa_considerations) to act as your firewall to allow required network traffic and to block unwanted network traffic.
      3. [Open up the required private IP addresses and ports](/docs/openshift?topic=openshift-firewall#firewall_outbound) for each region so that the master and the worker nodes can communicate and for the {{site.data.keyword.cloud_notm}} services that you plan to use.

<br />


## Deciding on your cluster setup
{: #prepare_cluster_level}

After you set up your account to create clusters, decide on the setup for your cluster. You must make these decisions every time that you create a cluster. You can click on the options in the following decision tree image for more information, such as comparisons of free and standard, Kubernetes and OpenShift, or VPC and classic clusters.
{: shortdesc}

<p class="note">OpenShift clusters are available only as standard clusters. You cannot get a [free](/docs/openshift?topic=openshift-faqs#openshift_free) OpenShift cluster.</p>


<img usemap="#cluster-plan-map" border="0" class="image" src="images/cluster-plan-dt.png" alt="This image walks you through choosing the setup that you want for your cluster."/>
<map name="cluster-plan-map">
    <area target="" alt="Free and standard cluster comparison" title="Free and standard cluster comparison" href="/docs/containers?topic=containers-cs_ov#cluster_types" coords="43,9,361,106" shape="rect">
    <area target="" alt="OpenShift and Kubernetes comparison" title="OpenShift and Kubernetes comparison" href="/docs/openshift?topic=openshift-cs_ov#openshift_kubernetes" coords="110,128,467,224" shape="rect">
    <area target="" alt="VPC and classic infrastructure comparison" title="VPC and classic infrastructure comparison" href="/docs/containers?topic=containers-infrastructure_providers" coords="60,252,398,352" shape="rect">
    <area target="" alt="Locations" title="Locations" href="/docs/containers?topic=containers-regions-and-zones#zones" coords="101,377,564,456" shape="rect">
    <area target="" alt="Virtual Machines" title="Virtual Machines" href="/docs/containers?topic=containers-planning_worker_nodes#vm" coords="105,488,564,538" shape="rect">
    <area target="" alt="Bare metal machines" title="Bare metal machines" href="/docs/containers?topic=containers-planning_worker_nodes#bm" coords="566,569,372,546" shape="rect">
    <area target="" alt="VPC scenarios" title="VPC scenarios" href="/docs/containers?topic=containers-plan_clusters#vpc-scenarios" coords="104,597,298,675" shape="rect">
    <area target="" alt="Classic scenarios" title="Classic scenarios" href="/docs/containers?topic=containers-plan_clusters#classic-scenarios" coords="369,596,566,674" shape="rect">
    <area target="" alt="Classic firewall" title="Classic firewall" href="/docs/containers?topic=containers-firewall" coords="369,681,564,704" shape="rect">
    <area target="" alt="VPC ACLs and firewall" title="VPC ACLs and firewall" href="/docs/containers?topic=containers-firewall" coords="103,680,298,704" shape="rect">
    <area target="" alt="Estimate costs (cluster create page)" title="Estimate costs (cluster create page)" href="https://cloud.ibm.com/kubernetes/catalog/cluster/create" coords="248,732,426,776" shape="rect">
</map>
<ff-roks311-vpc>
<img usemap="#cluster-plan-map" border="0" class="image" src="images/cluster-plan-dt-vpc.png" alt="This image walks you through choosing the setup that you want for your cluster."/>
<map name="cluster-plan-map">
    <area target="" alt="Free and standard cluster comparison" title="Free and standard cluster comparison" href="/docs/containers?topic=containers-cs_ov#cluster_types" coords="43,9,361,106" shape="rect">
    <area target="" alt="OpenShift and Kubernetes comparison" title="OpenShift and Kubernetes comparison" href="/docs/openshift?topic=openshift-cs_ov#openshift_kubernetes" coords="110,128,467,224" shape="rect">
    <area target="" alt="VPC and classic infrastructure comparison" title="VPC and classic infrastructure comparison" href="/docs/containers?topic=containers-infrastructure_providers" coords="60,252,398,352" shape="rect">
    <area target="" alt="Locations" title="Locations" href="/docs/containers?topic=containers-regions-and-zones#zones" coords="101,377,564,456" shape="rect">
    <area target="" alt="Virtual Machines" title="Virtual Machines" href="/docs/containers?topic=containers-planning_worker_nodes#vm" coords="105,488,564,538" shape="rect">
    <area target="" alt="Bare metal machines" title="Bare metal machines" href="/docs/containers?topic=containers-planning_worker_nodes#bm" coords="566,569,372,546" shape="rect">
    <area target="" alt="VPC scenarios" title="VPC scenarios" href="/docs/containers?topic=containers-plan_clusters#vpc-scenarios" coords="104,597,298,675" shape="rect">
    <area target="" alt="Classic scenarios" title="Classic scenarios" href="/docs/containers?topic=containers-plan_clusters#classic-scenarios" coords="369,596,566,674" shape="rect">
    <area target="" alt="Classic firewall" title="Classic firewall" href="/docs/containers?topic=containers-firewall" coords="369,681,564,704" shape="rect">
    <area target="" alt="VPC ACLs and firewall" title="VPC ACLs and firewall" href="/docs/containers?topic=containers-firewall" coords="103,680,298,704" shape="rect">
    <area target="" alt="Estimate costs (cluster create page)" title="Estimate costs (cluster create page)" href="https://cloud.ibm.com/kubernetes/catalog/cluster/create" coords="248,732,426,776" shape="rect">
</map></ff-roks311-vpc>

<br />


<ff-roks311-vpc>

## Creating a standard classic cluster
{: #clusters_standard}

Use the {{site.data.keyword.cloud_notm}} CLI or the {{site.data.keyword.cloud_notm}} console to create a fully-customizable standard cluster with your choice of hardware isolation and access to features like multiple worker nodes for a highly available environment.
{: shortdesc}

</ff-roks311-vpc>

##<ff-roks311-vpc>#</ff-roks311-vpc> Creating a standard classic cluster in the console
{: #clusters_ui}

Create your single zone or multizone classic OpenShift cluster by using the {{site.data.keyword.cloud_notm}} console.
{: shortdesc}

1. Make sure that you complete the prerequisites to [prepare your account](#cluster_prepare) and decide on your [cluster setup](#prepare_cluster_level).
2. From the [{site.data.keyword.cloud_notm}} Red Hat OpenShift on IBM Cloud Clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, click **Create cluster**.
3. Configure your cluster environment.
   3. Select **Classic infrastructure**.
   4. Give your cluster a unique name. The name must start with a letter, can contain letters, numbers, and hyphen (-), and must be 35 characters or fewer. Use a name that is unique across regions. The cluster name and the region in which the cluster is deployed form the fully qualified domain name for the Ingress subdomain. To ensure that the Ingress subdomain is unique within a region, the cluster name might be truncated and appended with a random value within the Ingress domain name.
 **Note**: Changing the unique ID or domain name that is assigned during cluster creation blocks the OpenShift master from managing your cluster.
   5. Select a resource group in which to create your cluster.
      * A cluster can be created in only one resource group, and after the cluster is created, you can't change its resource group.
      * To create clusters in a resource group other than the default, you must have at least the [**Viewer** role](/docs/openshift?topic=openshift-users#platform) for the resource group.
   6. Select a geography in which to deploy your cluster.
4. Select **Single zone** or **Multizone** availability. In a multizone cluster, the OpenShift master is deployed in a multizone-capable zone and three replicas of your master are spread across zones.
5. Enter your metro city and zone details.
  * Multizone clusters:
    1. Select a metro location. For the best performance, select the metro location that is physically closest to you. Your choices might be limited by geography.
    2. Select the specific zones in which you want to host your cluster. You must select at least one zone but you can select as many as you like. If you select more than one zone, the worker nodes are spread across the zones that you choose which gives you higher availability. If you select only one zone, you can [add zones to your cluster](/docs/openshift?topic=openshift-add_workers#add_zone) after the cluster is created.
  * Single zone clusters: Select a zone in which you want to host your cluster. For the best performance, select the zone that is physically closest to you. Your choices might be limited by geography.
6. For each of the selected zones, choose your public and private VLANs.
  * To create a cluster in which you can run internet-facing workloads:
    1. Select a public VLAN and a private VLAN from your IBM Cloud infrastructure account for each zone. Worker nodes communicate with each other by using the private VLAN, and can communicate with the OpenShift master by using the public or the private VLAN. If you do not have a public or private VLAN in this zone, a public and a private VLAN are automatically created for you. You can use the same VLAN for multiple clusters.
7. For **Master service endpoint**, choose how your OpenShift master and worker nodes communicate.
  * To create a cluster in which you can run internet-facing workloads:
    * If VRF and service endpoints are enabled in your {{site.data.keyword.cloud_notm}} account, select **Both private & public endpoints**.
    * If you cannot or do not want to enable VRF, select **Public endpoint only**.
  * To create a cluster that extends your on-premises data center only, or a cluster that extends your on-premises data center and provides limited public access with edge worker nodes, select **Both private & public endpoints** or **Private endpoint only**. Ensure that you have enabled VRF and service endpoints in your {{site.data.keyword.cloud_notm}} account. Note that if you enable the private service endpoint only, you must [expose the master endpoint through a private network load balancer](/docs/openshift?topic=openshift-access_cluster#access_private_se) so that users can access the master through a VPN or {{site.data.keyword.BluDirectLink}} connection.
  * To create a cluster that extends your on-premises data center and provides limited public access with a gateway appliance, select **Public endpoint only**.
8. Configure your default worker pool. Worker pools are groups of worker nodes that share the same configuration. You can always add more worker pools to your cluster later.
   1. Filter the worker flavors by selecting a machine type. Virtual is billed hourly and bare metal is billed monthly.
      - **Bare metal**: Bare metal servers are provisioned manually by IBM Cloud infrastructure after you order, and can take more than one business day to complete. Bare metal is best suited for high-performance applications that need more resources and host control. Be sure that you want to provision a bare metal machine. Because it is billed monthly, if you cancel it immediately after an order by mistake, you are still charged the full month.
      - **Virtual - shared**: Infrastructure resources, such as the hypervisor and physical hardware, are shared across you and other IBM customers, but each worker node is accessible only by you. Although this option is less expensive and sufficient in most cases, you might want to verify your performance and infrastructure requirements with your company policies.
      - **Virtual - dedicated**: Your worker nodes are hosted on infrastructure that is devoted to your account. Your physical resources are completely isolated.
   2. Select a flavor. The flavor defines the amount of virtual CPU, memory, and disk space that is set up in each worker node and made available to the containers. Available bare metal and virtual machines types vary by the zone in which you deploy the cluster. For more information, see [Planning your worker node setup](/docs/openshift?topic=openshift-planning_worker_nodes). After you create your cluster, you can add different flavors by adding a worker node or worker pool to the cluster.
   3. Specify the number of worker nodes that you need in the cluster. The number of workers that you enter is replicated across the number of zones that you selected. For example, if you selected two zones and want to create three worker nodes, a total of six worker nodes are provisioned in your cluster with three worker nodes in each zone.
9. Click **Create cluster**. A worker pool is created with the number of workers that you specified. You can see the progress of the worker node deployment in the **Worker nodes** tab.
    *   Your cluster might take some time to provision the OpenShift master and all worker nodes and enter a **Normal** state. Note that even if the cluster is ready, some parts of the cluster that are used by other services, such as Ingress secrets or registry image pull secrets, might still be in process. Wait until the cluster is ready before continuing to the next step by checking that the **Ingress subdomain** follows a pattern of `<cluster_name>.<region>.containers.appdomain.cloud`.
    *   Every worker node is assigned a unique worker node ID and domain name that must not be changed manually after the cluster is created. Changing the ID or domain name prevents the OpenShift master from managing your cluster.<p class="tip">Is your cluster not in a **Normal** state? Check out the [Debugging clusters](/docs/containers?topic=containers-cs_troubleshoot) guide for help. For example, if your cluster is provisioned in an account that is protected by a firewall gateway appliance, you must [configure your firewall settings to allow outgoing traffic to the appropriate ports and IP addresses](/docs/openshift?topic=openshift-firewall#firewall_outbound).</p>
10. After your cluster is created, you can [begin working with your cluster by configuring your CLI session](/docs/openshift?topic=openshift-access_cluster).

<br />


##<ff-roks311-vpc>#</ff-roks311-vpc> Creating a standard classic cluster in the CLI
{: #clusters_cli_steps}

Create your single zone or multizone classic cluster by using the {{site.data.keyword.cloud_notm}} CLI.
{: shortdesc}

**Before you begin**:
* Make sure that you complete the prerequisites to [prepare your account](#cluster_prepare) and decide on your [cluster setup](#prepare_cluster_level).
* Install the {{site.data.keyword.cloud_notm}} CLI and the [{{site.data.keyword.containerlong_notm}} plug-in](/docs/containers?topic=containers-cs_cli_install#cs_cli_install).

<br>

**To create a classic cluster from the CLI**:

1. Log in to the {{site.data.keyword.cloud_notm}} CLI.
   1. Log in and enter your {{site.data.keyword.cloud_notm}} credentials when prompted. If you have a federated ID, use `ibmcloud login --sso` to log in to the {{site.data.keyword.cloud_notm}} CLI.
      ```
      ibmcloud login [--sso]
      ```
      {: pre}

   2. If you have multiple {{site.data.keyword.cloud_notm}} accounts, select the account where you want to create your Kubernetes cluster.
   3. To create clusters in a resource group other than default, target that resource group.
      * A cluster can be created in only one resource group, and after the cluster is created, you can't change its resource group.
      * You must have at least the [**Viewer** role](/docs/openshift?topic=openshift-users#platform) for the resource group.

      ```
      ibmcloud target -g <resource_group_name>
      ```
      {: pre} 

3. Review the zones where you can create your cluster. In the output of the following command, zones have a **Location Type** of `dc`. To span your cluster across zones, you must create the cluster in a [multizone-capable zone](/docs/openshift?topic=openshift-regions-and-zones#zones). Multizone-capable zones have a metro value in the **Multizone Metro** column.
    ```
    ibmcloud oc supported-locations
    ```
    {: pre}
    When you select a zone that is located outside your country, keep in mind that you might require legal authorization before data can be physically stored in a foreign country.
    {: note}

4. Review the worker node flavors that are available in that zone. The flavor determines the amount of virtual CPU, memory, and disk space that is set up in each worker node and made available to your apps. Worker nodes in classic clusters can be created as virtual machines on shared or dedicated infrastructure, or as bare metal machines that are dedicated to you. For more information, see [Planning your worker node setup](/docs/openshift?topic=openshift-planning_worker_nodes). After you create your cluster, you can add different flavors by [adding a worker pool](/docs/openshift?topic=openshift-add_workers#add_pool).

   Before you create a bare metal machine, be sure that you want to provision one. Bare metal machines are billed monthly. If you order a bare metal machine by mistake, you are charged for the entire month, even if you cancel the machine immediately.  
   {:tip}

   ```
   ibmcloud oc flavors --zone <zone>
   ```
   {: pre}

5. Check if you have existing VLANs in the zones that you want to include in your cluster, and note the ID of the VLAN. If you do not have a public or private VLAN in one of the zones that you want to use in your cluster, {{site.data.keyword.containerlong_notm}} automatically creates these VLANs for you when you create the cluster.
   ```
   ibmcloud oc vlan ls --zone <zone>
   ```
   {: pre}

   Example output:
   ```
   ID        Name   Number   Type      Router
   1519999   vlan   1355     private   bcr02a.dal10
   1519898   vlan   1357     private   bcr02a.dal10
   1518787   vlan   1252     public    fcr02a.dal10
   1518888   vlan   1254     public    fcr02a.dal10
   ```
   {: screen}
   * To create a cluster in which you can run internet-facing workloads, check to see whether a public and private VLAN exist. If a public and private VLAN already exist, note the matching routers. Private VLAN routers always begin with <code>bcr</code> (back-end router) and public VLAN routers always begin with <code>fcr</code> (front-end router). When you create a cluster and specify the public and private VLANs, the number and letter combination after those prefixes must match. In the example output, any private VLAN can be used with any public VLAN because the routers all include `02a.dal10`.
   * To create a cluster that extends your on-premises data center on the private network only or provides limited public access through a gateway appliance, check to see whether a private VLAN exists. If you have a private VLAN, note the ID.

6. Create your standard cluster.
   * To create a cluster in which you can run internet-facing workloads:
     ```
     ibmcloud oc cluster create classic --zone <zone> --machine-type <flavor> --hardware <shared_or_dedicated> --public-vlan <public_VLAN_ID> --private-vlan <private_VLAN_ID> --workers <number> --name <cluster_name> --kube-version <major.minor.patch>_openshift [--private-service-endpoint] [--public-service-endpoint] [--disable-disk-encrypt]
     ```
     {: pre}

   <table>
   <caption>`cluster create classic` command components</caption>
   <thead>
   <th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding this command's components</th>
   </thead>
   <tbody>
   <tr>
   <td><code>cluster-create</code></td>
   <td>The command to create a cluster in your {{site.data.keyword.cloud_notm}} organization.</td>
   </tr>
   <tr>
   <td><code>--zone <em>&lt;zone&gt;</em></code></td>
   <td>Specify the {{site.data.keyword.cloud_notm}} zone ID that you chose earlier and that you want to use to create your cluster.</td>
   </tr>
   <tr>
   <td><code>--machine-type <em>&lt;flavor&gt;</em></code></td>
   <td>Specify the flavor for your worker node that you chose earlier.</td>
   </tr>
   <tr>
   <td><code>--hardware <em>&lt;shared_or_dedicated&gt;</em></code></td>
   <td>Specify with the level of hardware isolation for your worker node. Use <code>dedicated</code> to have available physical resources dedicated to you only, or <code>shared</code> to allow physical resources to be shared with other IBM customers. The default is shared. This value is optional for VM standard clusters. For bare metal flavors, specify <code>dedicated</code>.</td>
   </tr>
   <tr>
   <td><code>--public-vlan <em>&lt;public_vlan_id&gt;</em></code></td>
   <td>If you already have a public VLAN set up in your IBM Cloud infrastructure account for that zone, enter the ID of the public VLAN that you retrieved earlier. If you do not have a public VLAN in your account, do not specify this option. {{site.data.keyword.containerlong_notm}} automatically creates a public VLAN for you.<p>Private VLAN routers always begin with <code>bcr</code> (back-end router) and public VLAN routers always begin with <code>fcr</code> (front-end router). When you create a cluster and specify the public and private VLANs, the number and letter combination after those prefixes must match.</p></td>
   </tr>
   <tr>
   <td><code>--private-vlan <em>&lt;private_vlan_id&gt;</em></code></td>
   <td>If you already have a private VLAN set up in your IBM Cloud infrastructure account for that zone, enter the ID of the private VLAN that you retrieved earlier. If you do not have a private VLAN in your account, do not specify this option. {{site.data.keyword.containerlong_notm}} automatically creates a private VLAN for you.<p>Private VLAN routers always begin with <code>bcr</code> (back-end router) and public VLAN routers always begin with <code>fcr</code> (front-end router). When you create a cluster and specify the public and private VLANs, the number and letter combination after those prefixes must match.</p></td>
   </tr>
   <tr>
   <td><code>--private-only</code></td>
   <td>Create the cluster with private VLANs only. If you include this option, do not include the <code>--public-vlan</code> option.</td>
   </tr>
   <tr>
   <td><code>--name <em>&lt;name&gt;</em></code></td>
   <td>Specify a name for your cluster. The name must start with a letter, can contain letters, numbers, and hyphen (-), and must be 35 characters or fewer. Use a name that is unique across regions. The cluster name and the region in which the cluster is deployed form the fully qualified domain name for the Ingress subdomain. To ensure that the Ingress subdomain is unique within a region, the cluster name might be truncated and appended with a random value within the Ingress domain name.
</td>
   </tr>
   <tr>
   <td><code>--workers <em>&lt;number&gt;</em></code></td>
   <td>Specify the number of worker nodes to include in the cluster. If the <code>--workers</code> option is not specified, one worker node is created.</td>
   </tr>
   <tr>
   <td><code>--kube-version <em>&lt;major.minor.patch&gt;</em></code></td>
   <td>The OpenShift version for the cluster master node. This value is required. When the version is not specified, the cluster is created with the default supported Kubernetes version. If you do not specify a supported OpenShift version, your cluster is created as a community Kubernetes cluster. To see available versions, run <code>ibmcloud oc versions</code>.
</td>
   </tr>
   <tr>
   <td><code>--private-service-endpoint</code></td>
   <td>**In [VRF-enabled accounts](/docs/resources?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud)**: Enable the private service endpoint so that your OpenShift master and the worker nodes can communicate over the private VLAN. In addition, enable the public service endpoint by using the `--public-service-endpoint` flag to access your cluster over the internet. After you enable a private service endpoint, you cannot later disable it.<br><br>After you create the cluster, you can get the endpoint by running `ibmcloud oc cluster get --cluster <cluster_name_or_ID>`.</td>
   </tr>
   <tr>
   <td><code>--public-service-endpoint</code></td>
   <td>Enable the public service endpoint so that your OpenShift master can be accessed over the public network, for example to run `oc` commands from your terminal, and so that your OpenShift master and the worker nodes can communicate over the public VLAN.<br><br>After you create the cluster, you can get the endpoint by running `ibmcloud oc cluster get --cluster <cluster_name_or_ID>`.</td>
   </tr>
   <tr>
   <td><code>--disable-disk-encrypt</code></td>
   <td>Worker nodes feature AES 256-bit [disk encryption](/docs/containers?topic=containers-security#encrypted_disk) by default. If you want to disable encryption, include this option.</td>
   </tr>
   </tbody></table>

7. Verify that the creation of the cluster was requested. For virtual machines, it can take a few minutes for the worker node machines to be ordered, and for the cluster to be set up and provisioned in your account. Bare metal physical machines are provisioned by manual interaction with IBM Cloud infrastructure, and can take more than one business day to complete.
   ```
   ibmcloud oc cluster ls
   ```
   {: pre}

   When the provisioning of your OpenShift master is completed, the **State** of your cluster changes to `deployed`. After your OpenShift master is ready, the provisioning of your worker nodes is initiated.
   ```
   Name         ID                         State      Created          Workers    Zone      Version     Resource Group Name   Provider
   mycluster    blrs3b1d0p0p2f7haq0g       deployed   20170201162433   3          dal10     3.11.154_xxxx_openshift      Default             classic
   ```
   {: screen}

   Is your cluster not in a `deployed` state? Check out the [Debugging clusters](/docs/containers?topic=containers-cs_troubleshoot) guide for help. For example, if your cluster is provisioned in an account that is protected by a firewall gateway appliance, you must [configure your firewall settings to allow outgoing traffic to the appropriate ports and IP addresses](/docs/openshift?topic=openshift-firewall#firewall_outbound).
   {: tip}

8. Check the status of the worker nodes.
   ```
   ibmcloud oc worker ls --cluster <cluster_name_or_ID>
   ```
   {: pre}

   When the worker nodes are ready, the worker node state changes to **normal** and the status changes to **Ready**. When the node status is **Ready**, you can then access the cluster. Note that even if the cluster is ready, some parts of the cluster that are used by other services, such as Ingress secrets or registry image pull secrets, might still be in process. Note that if you created your cluster with a private VLAN only, no **Public IP** addresses are assigned to your worker nodes.
   ```
   ID                                                     Public IP        Private IP     Flavor              State    Status   Zone    Version
   kube-blrs3b1d0p0p2f7haq0g-mycluster-default-000001f7   169.xx.xxx.xxx  10.xxx.xx.xxx   u3c.2x4.encrypted   normal   Ready    dal10   1.14.9
   ```
   {: screen}

   Every worker node is assigned a unique worker node ID and domain name that must not be changed manually after the cluster is created. Changing the ID or domain name prevents the OpenShift master from managing your cluster.
   {: important}

9. After your cluster is created, you can [begin working with your cluster by configuring your CLI session](/docs/openshift?topic=openshift-access_cluster).

<br />




<br />


<ff-roks311-vpc>

## Creating a standard VPC Gen 1 compute cluster
{: #clusters_vpc_standard}

Use the {{site.data.keyword.cloud_notm}} CLI or the {{site.data.keyword.cloud_notm}} console to create a standard VPC Generation 1 compute cluster, and customize your cluster to meet the high availability and security requirements of your apps.
{: shortdesc}

### Creating a standard VPC Gen 1 compute cluster in the console
{: #clusters_vpc_ui}

Create your single zone or multizone VPC Generation 1 compute cluster by using the {{site.data.keyword.cloud_notm}} console.
{: shortdesc}

1. Make sure that you complete the prerequisites to [prepare your account](#cluster_prepare) and decide on your [cluster setup](#prepare_cluster_level).
2. [Create a Virtual Private Cloud (VPC) ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/vpc/provision/vpc) with a subnet that is located in the VPC zone where you want to create the cluster. During the VPC creation, you can create one subnet only. Subnets are specific to a zone. If you want to create a multizone cluster, create the subnet in one of the multizone-capable zones that you want to use. Later, you manually create the subnets for the remaining zones that you want to include in your cluster. For more information, see [Creating a VPC using the IBM Cloud console](/docs/vpc-on-classic?topic=vpc-on-classic-creating-a-vpc-using-the-ibm-cloud-console).
3. If you want to create a multizone cluster, create the subnets for all of the remaining zones that you want to include in your cluster. You must have one VPC subnet in all of the zones where you want to create your multizone cluster.
   1. From the [VPC subnet dashboard](https://cloud.ibm.com/vpc/network/subnets), click **New subnet**.
   2. Enter a name for your subnet and select the name of the VPC that you created.
   3. Select the location and zone where you want to create the subnet.
   4. Specify the number of IP addresses to create. VPC subnets provide IP addresses for your worker nodes and load balancer services in the cluster, so create a VPC subnet with enough IP addresses, such as 256. You cannot change the number of IPs that a VPC subnet has later. If you enter a specific IP range, do not use the following reserved ranges: `172.16.0.0/16`, `172.18.0.0/16`, `172.19.0.0/16`, and `172.20.0.0/16`.
   5. Choose if you want to attach a public network gateway to your subnet. A public network gateway is required when you want your cluster to access public endpoints, such as a public URL of another app, or an {{site.data.keyword.cloud_notm}} service that supports public service endpoints only. Make sure to review the [VPC networking basics](/docs/openshift?topic=openshift-plan_clusters#vpc_basics) to understand when a public network gateway is required and how you can set up your cluster to limit public access to one or more subnets only.
   6. Click **Create subnet**.  
4. From the [{{site.data.keyword.containerlong_notm}} dashboard ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/kubernetes/clusters), click **Create cluster**.
5. Configure your cluster environment.
   3. Select **VPC infrastructure**.
   4. From the **Virtual Private Cloud** drop-down menu, select the VPC that you created earlier.
   5. Give your cluster a unique name. The name must start with a letter, can contain letters, numbers, and hyphen (-), and must be 35 characters or fewer. Use a name that is unique across regions. The cluster name and the region in which the cluster is deployed form the fully qualified domain name for the Ingress subdomain. To ensure that the Ingress subdomain is unique within a region, the cluster name might be truncated and appended with a random value within the Ingress domain name.
 **Note**: Changing the unique ID or domain name that is assigned during cluster creation blocks the OpenShift master from managing your cluster.
   6. Select a resource group in which to create your cluster.
      * A cluster can be created in only one resource group, and after the cluster is created, you can't change its resource group.
      * To create clusters in a resource group other than the default, you must have at least the [**Viewer** role](/docs/openshift?topic=openshift-users#platform) for the resource group.
      * The cluster can be in a different resource group than the VPC.
   7. Select a geography in which to deploy your cluster.
6. Select the location to deploy your cluster and set up your cluster for high availability.
   1. Select the metro city location where you want to create your cluster. For the best performance, select the location that is physically closest to you. Your choices might be limited by the geography that you selected.
   2. Select the worker node zones where you want to create worker nodes. To create a [single zone cluster](/docs/openshift?topic=openshift-ha_clusters#single_zone), select one zone only. To create a [multizone cluster](/docs/openshift?topic=openshift-ha_clusters#multizone), select multiple zones.
   3. For each of the selected zones, choose the VPC subnet that you want to use for your worker nodes. The VPC subnets that you created earlier are automatically loaded for the selected worker node zones.
7. Configure your cluster with a public and a private service endpoint by setting the **Master service endpoint**. For more information about what setup is required to run internet-facing apps, or to keep your cluster private, see [Planning your cluster network setup](/docs/openshift?topic=openshift-plan_clusters#vpc-pgw).
8. Configure your default worker pool. Worker pools are groups of worker nodes that share the same configuration. You can always add more worker pools to your cluster later.
   1. Use the filter options to limit the number of shared virtual server flavors that are displayed to you.
   2. Select a flavor. The flavor determines the amount of virtual CPU, memory, and disk space that is set up in each worker node and made available to your apps. VPC Gen 1 worker nodes can be created as virtual machines on shared infrastructure only. Bare metal or software-defined storage machines are not supported. For more information, see [Planning your worker node setup](/docs/openshift?topic=openshift-planning_worker_nodes). After you create your cluster, you can add different flavors by adding a worker node or worker pool to the cluster.
   3. Specify the number of worker nodes that you need in the cluster. The number of workers that you enter is replicated across the number of zones that you selected. For example, if you selected two zones and want to create three worker nodes, a total of six worker nodes are provisioned in your cluster with three worker nodes in each zone.
9. Click **Create cluster**. A worker pool is created with the number of workers that you specified. You can see the progress of the worker node deployment in the **Worker nodes** tab.
   - When the deployment is done, you can see that your cluster is ready in the **Overview** tab. Note that even if the cluster is ready, some parts of the cluster that are used by other services, such as Ingress secrets or registry image pull secrets, might still be in process. Wait until the cluster is ready before continuing to the next step by checking that the **Ingress subdomain** follows a pattern of `<cluster_name>.<region>.containers.appdomain.cloud`.
   - Every worker node is assigned a unique worker node ID and domain name that must not be changed manually after the cluster is created. Changing the ID or domain name prevents the OpenShift master from managing your cluster.<p class="tip">Is your cluster not in a **deployed** state? Check out the [Debugging clusters](/docs/containers?topic=containers-cs_troubleshoot) guide for help. For example, if your cluster is provisioned in an account that is protected by a firewall gateway appliance, you must [configure your firewall settings to allow outgoing traffic to the appropriate ports and IP addresses](/docs/openshift?topic=openshift-firewall#firewall_outbound).</p>
10. After your cluster is created, you can [begin working with your cluster by configuring your CLI session](/docs/openshift?topic=openshift-access_cluster).

### Creating standard VPC Gen 1 compute clusters from the CLI
{: #cluster_vpc_cli}

Create your single zone or multizone VPC Generation 1 compute cluster by using the {{site.data.keyword.cloud_notm}} CLI.
{: shortdesc}

**Before you begin**:
* Make sure that you complete the prerequisites to [prepare your account](#cluster_prepare) and decide on your [cluster setup](#prepare_cluster_level).
* Install the {{site.data.keyword.cloud_notm}} CLI and the [{{site.data.keyword.containerlong_notm}} plug-in](/docs/containers?topic=containers-cs_cli_install#cs_cli_install).
* Install the [VPC CLI plug-in](/docs/vpc-on-classic?topic=vpc-infrastructure-cli-plugin-vpc-reference#prerequisites-).

<br>

**To create a VPC cluster from the CLI**:

1. In your terminal, log in to your {{site.data.keyword.cloud_notm}} account and target the {{site.data.keyword.cloud_notm}} region and resource group where you want to create your VPC cluster. For supported regions, see [Creating a VPC in a different region](/docs/vpc-on-classic?topic=vpc-on-classic-creating-a-vpc-in-a-different-region). The cluster's resource group can differ from the VPC resource group. Enter your {{site.data.keyword.cloud_notm}} credentials when prompted. If you have a federated ID, use the --sso flag to log in.
   ```
   ibmcloud login -r <region> [--sso]
   ```
   {: pre}

2. Target the {{site.data.keyword.cloud_notm}} infrastructure generation **1** for VPC.
   ```
   ibmcloud is target --gen 1
   ```
   {: pre}

3. [Create a VPC](/docs/vpc-on-classic?topic=vpc-on-classic-creating-a-vpc-using-the-ibm-cloud-cli#step-3-create-a-vpc-and-save-the-vpc-id) in the same region where you want to create the cluster.
4. [Create a subnet for your VPC](/docs/vpc-on-classic?topic=vpc-on-classic-creating-a-vpc-using-the-ibm-cloud-cli#step-4-create-a-subnet-and-save-the-subnet-id).
  * If you want to create a [multizone cluster](/docs/openshift?topic=openshift-ha_clusters#multizone), repeat this step to create additional subnets in all of the zones that you want to include in your cluster.
  * VPC subnets provide IP addresses for your worker nodes and load balancer services in the cluster, so create a VPC subnet with enough IP addresses, such as 256. You cannot change the number of IPs that a VPC subnet has later.
  * Do not use the following reserved ranges: `172.16.0.0/16`, `172.18.0.0/16`, `172.19.0.0/16`, and `172.20.0.0/16`.
5.  Create the cluster in your VPC. You can use the `cluster create vpc-classic` command to create a single zone cluster in your VPC with worker nodes that are connected to one VPC subnet only. If you want to create a multizone cluster, you can use the {{site.data.keyword.cloud_notm}} console, or [add more zones](/docs/openshift?topic=openshift-add_workers) to your cluster after the cluster is created. The cluster takes a few minutes to provision.
    ```
    ibmcloud oc cluster create vpc-classic --name <cluster_name> --zone <vpc_zone> --vpc-id <vpc_ID> --subnet-id <vpc_subnet_ID> --flavor <worker_flavor> --kube-version <major.minor.patch> --provider vpc-classic [--workers <number_workers_per_zone>] 
    ```
    {: pre}

    <table>
    <caption>Cluster create components</caption>
    <thead>
    <th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding this command's components</th>
    </thead>
    <tbody>
    <tr>
    <td><code>cluster create vpc-classic</code></td>
    <td>The command to create a standard VPC Gen 1 compute cluster in your {{site.data.keyword.cloud_notm}} organization.</td>
    </tr>
    <tr>
    <td><code>--name <em>&lt;cluster_name&gt;</em></code></td>
    <td>Specify a name for your cluster. The name must start with a letter, can contain letters, numbers, and hyphen (-), and must be 35 characters or fewer. Use a name that is unique across regions. The cluster name and the region in which the cluster is deployed form the fully qualified domain name for the Ingress subdomain. To ensure that the Ingress subdomain is unique within a region, the cluster name might be truncated and appended with a random value within the Ingress domain name.
</td>
    </tr>
    <tr>
    <td><code>--zone <em>&lt;zone&gt;</em></code></td>
    <td>Specify the {{site.data.keyword.cloud_notm}} zone where you want to create your cluster. Make sure that you use a zone that matches the metro city location that you selected when you created your VPC and that you have an existing VPC subnet for that zone. For example, if you created your VPC in the Dallas metro city, your zone must be set to <code>us-south-1</code>, <code>us-south-2</code>, or <code>us-south-3</code>. To list available VPC cluster zones, run <code>ibmcloud oc zone ls --provider vpc-classic</code>. Note that when you select a zone outside of your country, you might require legal authorization before data can be physically stored in a foreign country.</td>
    </tr>
    <tr>
    <td><code>--vpc-id <em>&lt;vpc_ID&gt;</em></code></td>
    <td>Enter the ID of the VPC that you created earlier. To retrieve the ID of your VPC, run <code>ibmcloud oc vpcs</code>. </td>
    </tr>
    <tr>
    <td><code>--subnet-id <em>&lt;subnet_ID&gt;</em></code></td>
    <td>Enter the ID of the VPC subnet that you created earlier. When you create a VPC cluster from the CLI, you can initially create your cluster in one zone with one subnet only. To create a multizone cluster, [add more zones](/docs/openshift?topic=openshift-add_workers) with the subnets that you created earlier to your cluster after the cluster is created. To list the IDs of your subnets, run <code> ibmcloud oc subnets --provider vpc-classic --vpc-id &lt,VPC_ID&gt; --zone &lt;subnet_zone&gt; </code>.  </td>
    </tr>
    <tr>
    <td><code>--flavor <em>&lt;worker_flavor&gt;</em></code></td>
    <td>Enter the worker node flavor that you want to use. The flavor determines the amount of virtual CPU, memory, and disk space that is set up in each worker node and made available to your apps. VPC Gen 1 worker nodes can be created as virtual machines on shared infrastructure only. Bare metal or software-defined storage machines are not supported.  For more information, see [Planning your worker node setup](/docs/openshift?topic=openshift-planning_worker_nodes). To view available flavors, first list available VPC zones with <code>ibmcloud oc zone ls --provider vpc-classic</code>, and then use the zone to list supported flavors by running <code>ibmcloud oc flavors --zone &lt;VPC_zone&gt;</code>. After you create your cluster, you can add different flavors by adding a worker node or worker pool to the cluster.</td>
    </tr>
    <tr>
    <td><code>--kube-version <em>&lt;major.minor.patch&gt;</em></code></td>
    <td>The OpenShift version for the cluster master node. This value is required. When the version is not specified, the cluster is created with the default supported Kubernetes version. If you do not specify a supported OpenShift version, your cluster is created as a community Kubernetes cluster. To see available versions, run <code>ibmcloud oc versions</code>.
</td>
    </tr>  
    <tr>
    <td><code>--provider <em>&lt;vpc-classic&gt;</em></code></td>
    <td>Enter the generation of {{site.data.keyword.cloud_notm}} infrastructure that you want to use. To create a VPC Generation 1 compute cluster, you must enter <strong>vpc-classic</strong>.</td>
    </tr>
    <tr>
    <td><code>--workers <em>&lt;number&gt;</em></code></td>
    <td>Specify the number of worker nodes to include in the cluster. If the <code>--workers</code> option is not specified, one worker node is created by default.</td>
    </tr>
    </tbody></table>
6. Verify that the creation of the cluster was requested. It can take a few minutes for the worker node machines to be ordered, and for the cluster to be set up and provisioned in your account.
    ```
    ibmcloud oc cluster ls
    ```
    {: pre}

    When the provisioning of your OpenShift master is completed, the status of your cluster changes to **deployed**. After the OpenShift master is ready, your worker nodes are set up.
    ```
    Name         ID                                   State      Created          Workers    Zone      Version     Resource Group Name   Provider
    mycluster    aaf97a8843a29941b49a598f516da72101   deployed   20170201162433   3          mil01     1.14.9      Default             classic
    ```
    {: screen}

    Is your cluster not in a **deployed** state? Check out the [Debugging clusters](/docs/containers?topic=containers-cs_troubleshoot) guide for help. For example, if your cluster is provisioned in an account that is protected by a firewall gateway appliance, you must [configure your firewall settings to allow outgoing traffic to the appropriate ports and IP addresses](/docs/openshift?topic=openshift-firewall#firewall_outbound).
    {: tip}

7. Check the status of the worker nodes.
   ```
   ibmcloud oc worker ls --cluster <cluster_name_or_ID>
   ```
   {: pre}

   When the worker nodes are ready, the worker node **State** changes to `deployed` and the **Status** changes to `Ready`. When the node **Status** changes to `Ready`, you can access the cluster. Note that even if the cluster is ready, some parts of the cluster that are used by other services, such as Ingress secrets or registry image pull secrets, might still be in process.
   ```
   ID                                                     Public IP        Private IP     Flavor              State    Status   Zone    Version
   kube-blrs3b1d0p0p2f7haq0g-mycluster-default-000001f7   169.xx.xxx.xxx  10.xxx.xx.xxx   u3c.2x4.encrypted   normal   Ready    dal10   1.14.9
   ```
   {: screen}

   Every worker node is assigned a unique worker node ID and domain name that must not be changed manually after the cluster is created. Changing the ID or domain name prevents the OpenShift master from managing your cluster.
   {: important}

8. After your cluster is created, you can [begin working with your cluster by configuring your CLI session](/docs/openshift?topic=openshift-access_cluster).

<br />


</ff-roks311-vpc>

## Next steps
{: #next_steps}

When the cluster is up and running, you can check out the following cluster administration tasks:
- If you created the cluster in a multizone capable zone, [spread worker nodes by adding a zone to your cluster](/docs/openshift?topic=openshift-add_workers). 
- [Deploy an app in your cluster.](/docs/containers?topic=containers-app#app_cli)
- [Set up your own private registry in {{site.data.keyword.cloud_notm}} to store and share Docker images with other users.](/docs/services/Registry?topic=registry-getting-started)
- [Set up the cluster autoscaler](/docs/openshift?topic=openshift-ca#ca) to automatically add or remove worker nodes from your worker pools based on your workload resource requests.
- Control who can create pods in your cluster with [pod security policies](/docs/containers?topic=containers-psp).

Then, you can check out the following network configuration steps for your cluster setup:
* Classic clusters:
  * Isolate networking workloads to edge worker nodes [in classic clusters without a gateway](/docs/openshift?topic=openshift-edge) or [in gateway-enabled classic clusters](/docs/openshift?topic=openshift-edge#edge_gateway).
  * Expose your apps with [public networking services](/docs/containers?topic=containers-cs_network_planning#public_access) or [private networking services](/docs/containers?topic=containers-cs_network_planning#private_access).
  * Connect your cluster with services in private networks outside of your {{site.data.keyword.cloud_notm}} account by setting up [{{site.data.keyword.cloud_notm}} Direct Link](/docs/infrastructure/direct-link?topic=direct-link-get-started-with-ibm-cloud-direct-link) or the [strongSwan IPSec VPN service](/docs/openshift?topic=openshift-vpn).
  * Create Calico host network policies to isolate your cluster on the [public network](/docs/openshift?topic=openshift-network_policies#isolate_workers_public) and on the [private network](/docs/openshift?topic=openshift-network_policies#isolate_workers).<ff-roks311-vpc>
* VPC clusters:
  * Expose your apps with [public networking services](/docs/containers?topic=containers-cs_network_planning#public_access) or [private networking services](/docs/containers?topic=containers-cs_network_planning#private_access).
  * [Connect your cluster with services in private networks outside of your {{site.data.keyword.cloud_notm}} account](/docs/openshift?topic=openshift-vpc-vpnaas) by setting up the {{site.data.keyword.cloud_notm}} VPC VPN or the strongSwan IPSec VPN service.
  * [Create access control lists (ACLs)](/docs/openshift?topic=openshift-vpc-network-policy) to control ingress and egress traffic to your VPC subnets.</ff-roks311-vpc>




# Creating OpenShift clusters
{: #clusters}

Create a {{site.data.keyword.openshiftlong}} cluster.
{: shortdesc}

## Prerequisites
{: #openshift_cluster_prereqs}

To create OpenShift clusters, complete the following prerequisite steps.

1.  [Prepare your account to create clusters](/docs/containers?topic=containers-clusters#cluster_prepare). This step includes creating a billable account, setting up an API key with infrastructure permissions, making sure that you have Administrator access in {{site.data.keyword.cloud_notm}} IAM, planning resource groups, and setting up account networking.
2.  [Prepare to create clusters](/docs/containers?topic=containers-clusters#prepare_cluster_level). This step includes planning cluster setup, estimating costs, and if applicable, allowing network traffic through a firewall.<p class="note">OpenShift clusters are available [only as standard cluster, not free](/docs/openshift?topic=openshift-faqs#openshift_free).</p>
3.   [Install the {{site.data.keyword.cloud_notm}} and OpenShift CLIs](/docs/openshift?topic=openshift-openshift-cli).

<br />


## Creating a<ff-roks311-vpc> classic</ff-roks311-vpc> cluster with the console
{: #openshift_create_cluster_console}

Create a standard OpenShift cluster in the {{site.data.keyword.cloud_notm}} console.
{: shortdesc}

Before you begin, [complete the prerequisites](#openshift_cluster_prereqs).

1.  Create a cluster.
    1.  Log in to your [{{site.data.keyword.cloud_notm}} account ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/).
    2.  From the hamburger menu ![hamburger menu icon](../icons/icon_hamburger.svg "hamburger menu icon"), select **OpenShift** and then click **Create cluster**.
    3.  Choose your cluster setup details and name.
    *   Fill out your cluster name, resource group, and tags.
    *   For the **Location**, set the **Geography**, and then select any of the six worldwide multizone **Metro** or single zone [locations](/docs/openshift?topic=openshift-regions-and-zones) to use for your **Worker zones**.
    *   For **Default worker pool**, choose an available flavor for your worker nodes. Red Hat OpenShift on IBM Cloud supports OpenShift version 3.11 only, which includes Kubernetes version 1.11. The operating system is Red Hat Enterprise Linux 7.
    1.  To finish, click **Create cluster**.<p class="note">Your cluster creation might take some time to complete. After the cluster state shows **Normal**, the cluster network and load-balancing components take about 10 more minutes to deploy and update the cluster domain that you use for the OpenShift web console and other routes. Wait until the cluster is ready before continuing to the next step by checking that the **Ingress subdomain** follows a pattern of `<cluster_name>.<globally_unique_account_HASH>-0001.<region>.containers.appdomain.cloud`.<br><br>If your cluster does not reach a **deployed** state, check out the [Debugging clusters](/docs/containers?topic=containers-cs_troubleshoot) guide for help. For example, if your cluster is provisioned in an account that is protected by a firewall gateway appliance, you must [configure your firewall settings to allow outgoing traffic to the appropriate ports and IP addresses](/docs/openshift?topic=openshift-firewall).</p>
2.  From the cluster details page, click **OpenShift web console**. For more information about using the OpenShift console, see the [OpenShift docs ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/getting_started/developers_console.html).
3.  To continue working in the terminal: From the OpenShift web console menu bar, click your profile **IAM#user.name@email.com > Copy Login Command**. Paste the copied `oc` login command into your terminal to authenticate via the CLI.

<br />


## Creating a cluster with the CLI
{: #openshift_create_cluster_cli}

Create a standard OpenShift cluster by using the {{site.data.keyword.cloud_notm}} CLI.
{: shortdesc}

Before you begin, [complete the prerequisites](#openshift_cluster_prereqs).

1.  Log in to the account that you set up to create OpenShift clusters. Target the **us-east** or **eu-gb** region and the resource group. If you have a federated account, include the `--sso` flag.
    ```
    ibmcloud login -r (us-east|eu-gb) [-g default] [--sso]
    ```
    {: pre}
2.  Create a cluster.
    ```
    ibmcloud oc cluster create classic --name <name> --location <zone> --kube-version <openshift_version> --machine-type <worker_node_flavor> --workers <number_of_worker_nodes_per_zone> --public-vlan <public_VLAN_ID> --private-vlan <private_VLAN_ID>
    ```
    {: pre}

    Example command to create a cluster with three workers nodes that have four cores and 16 GB memory in Washington, DC:

    ```
    ibmcloud oc cluster create classic --name my_openshift --location wdc04 --kube-version 3.11_openshift --machine-type b3c.4x16.encrypted  --workers 3 --public-vlan <public_VLAN_ID> --private-vlan <private_VLAN_ID>
    ```
    {: pre}

    <table summary="The first row in the table spans both columns. The rest of the rows should be read left to right, with the command component in column one and the matching description in column two.">
    <caption>cluster create components</caption>
    <thead>
    <th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding this command's components</th>
    </thead>
    <tbody>
    <tr>
    <td><code>cluster-create</code></td>
    <td>The command to create a classic infrastructure cluster in your {{site.data.keyword.cloud_notm}} account.</td>
    </tr>
    <tr>
    <td><code>--name <em>&lt;name&gt;</em></code></td>
    <td>Enter a name for your cluster. The name must start with a letter, can contain letters, numbers, and hyphens (-), and must be 35 characters or fewer. Use a name that is unique across {{site.data.keyword.cloud_notm}} regions.</td>
    </tr>
    <tr>
    <td><code>--location <em>&lt;zone&gt;</em></code></td>
    <td>Specify the zone where you want to create your cluster. For a list of supported zones, see [Single and multizone locations](/docs/openshift?topic=openshift-regions-and-zones#zones).</p></td>
    </tr>
    <tr>
      <td><code>--kube-version <em>&lt;openshift_version&gt;</em></code></td>
      <td>You must choose a supported OpenShift version. OpenShift versions include a Kubernetes version that differs from the Kubernetes versions that are available on community Kubernetes Ubuntu clusters. To list available OpenShift versions, run `ibmcloud oc versions`. To create a cluster with the latest the patch version, you can specify just the major and minor version, such as ` 3.11_openshift`.<br><br>Red Hat OpenShift on IBM Cloud supports OpenShift version 3.11 only, which includes Kubernetes version 1.11. The operating system is Red Hat Enterprise Linux 7.</td>
    </tr>
    <tr>
    <td><code>--machine-type <em>&lt;worker_node_flavor&gt;</em></code></td>
    <td>Choose a machine type, or flavor, for your worker nodes. You can deploy your worker nodes as virtual machines on shared or dedicated hardware, or as physical machines on bare metal. Available physical and virtual machines types vary by the zone in which you deploy the cluster. To list available flavors, run `ibmcloud oc flavors --zone <zone>`.</td>
    </tr>
    <tr>
    <td><code>--workers <em>&lt;number_of_worker_nodes_per_zone&gt;</em></code></td>
    <td>The number of worker nodes to include in the cluster. You might want to specify at least three worker nodes so that your cluster has enough resources to run the default components and for high availability. If the <code>--workers</code> option is not specified, one worker node is created.</td>
    </tr>
    <tr>
    <td><code>--public-vlan <em>&lt;public_vlan_id&gt;</em></code></td>
    <td>If you already have a public VLAN set up in your IBM Cloud infrastructure account for that zone, enter the ID of the public VLAN. To check available VLANs, run `ibmcloud oc vlan ls --zone <zone>`. <br><br>If you do not have a public VLAN in your account, do not specify this option. {{site.data.keyword.containerlong_notm}} automatically creates a public VLAN for you.</td>
    </tr>
    <tr>
    <td><code>--private-vlan <em>&lt;private_vlan_id&gt;</em></code></td>
    <td>If you already have a private VLAN set up in your IBM Cloud infrastructure account for that zone, enter the ID of the private VLAN. To check available VLANs, run `ibmcloud oc vlan ls --zone <zone>`. <br><br>If you do not have a private VLAN in your account, do not specify this option. {{site.data.keyword.containerlong_notm}} automatically creates a private VLAN for you.</td>
    </tr>
    </tbody></table>
3.  List your cluster details. Review the cluster **State**, check the **Ingress Subdomain**, and note the **Master URL**.<p class="note">Your cluster creation might take some time to complete. After the cluster state shows **Normal**, the cluster network and load-balancing components take about 10 more minutes to deploy and update the cluster domain that you use for the OpenShift web console and other routes. Wait until the cluster is ready before continuing to the next step by checking that the **Ingress Subdomain** follows a pattern of `<cluster_name>.<globally_unique_account_HASH>-0001.<region>.containers.appdomain.cloud`.<br><br>Is your cluster not in a **deployed** state? Check out the [Debugging clusters](/docs/containers?topic=containers-cs_troubleshoot) guide for help. For example, if your cluster is provisioned in an account that is protected by a firewall gateway appliance, you must [configure your firewall settings to allow outgoing traffic to the appropriate ports and IP addresses](/docs/openshift?topic=openshift-firewall).</p>

    ```
    ibmcloud oc cluster get --cluster <cluster_name_or_ID>
    ```
    {: pre}

4.  Download the configuration files to connect to your cluster.
    ```
    ibmcloud oc cluster config --cluster <cluster_name_or_ID>
    ```
    {: pre}

    When the download of the configuration files is finished, a command is displayed that you can copy and paste to set the path to the local Kubernetes configuration file as an environment variable.

    Example for OS X:

    ```
    export KUBECONFIG=/Users/<user_name>/.bluemix/plugins/kubernetes-service/clusters/<cluster_name>/kube-config-<datacenter>-<cluster_name>.yml
    ```
    {: screen}
5.  In your browser, navigate to the address of your **Master URL** and append `/console`. For example, `https://c0.containers.cloud.ibm.com:23652/console`.
6.  From the OpenShift web console menu bar, click your profile **IAM#user.name@email.com > Copy Login Command**. Paste the copied `oc` login command into your terminal to authenticate via the CLI.<p class="tip">Save your cluster master URL to access the OpenShift console later. In future sessions, you can skip the `cluster config` step and copy the login command from the console instead.</p>
7.  Verify that the `oc` commands run properly with your cluster by checking the version.

    ```
    oc version
    ```
    {: pre}

    Example output:

    ```
    oc v3.11.0+0cbc58b
    kubernetes v1.11.0+d4cacc0
    features: Basic-Auth

    Server https://c0.containers.cloud.ibm.com:23652
    openshift v3.11.98
    kubernetes v1.11.0+d4cacc0
    ```
    {: screen}

<br />


## Next steps
{: #next_steps}

When the cluster is up and running, you can check out the following tasks:
- If you created the cluster in a multizone capable zone, [spread worker nodes by adding a zone to your cluster](/docs/openshift?topic=openshift-add_workers).
- [Deploy an app in your cluster](/docs/openshift?topic=openshift-openshift_apps).
- [Expose your apps with routes](/docs/openshift?topic=openshift-openshift_routes).
