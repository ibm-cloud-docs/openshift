---

copyright:
  years: 2014, 2021
lastupdated: "2021-04-27"

keywords: openshift, roks, rhoks, rhos, clusters

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
 


# Creating {{site.data.keyword.openshiftshort}} clusters
{: #clusters}

Create a cluster in {{site.data.keyword.openshiftlong}}.
{: shortdesc}

After [getting started](/docs/containers?topic=containers-getting-started), you might want to create a cluster that is customized to your use case and different public and private cloud environments. Consider the following steps to create the right cluster each time.

1.  [Prepare your account to create clusters](/docs/openshift?topic=openshift-clusters#cluster_prepare). This step includes creating a billable account, setting up an API key with infrastructure permissions, making sure that you have Administrator access in {{site.data.keyword.cloud_notm}} IAM, planning resource groups, and setting up account networking.
2.  [Decide on your cluster setup](/docs/openshift?topic=openshift-clusters#prepare_cluster_level). This step includes planning cluster network and HA setup, estimating costs, and if applicable, allowing network traffic through a firewall.
3.  Create your [VPC Gen2](#clusters_vpcg2) or [classic](#clusters_standard) cluster by following the steps in the {{site.data.keyword.cloud_notm}} console or CLI.

<img src="images/icon-version-311.png" alt="Version 3.11 icon" width="30" style="width:30px; border-style: none"/> {{site.data.keyword.openshiftshort}} version 3.11 is deprecated, and becomes unsupported on 6 June 2022 (date subject to change). Instead, you can create a version 4 cluster.
{: deprecated}

<br />

## Sample commands
{: #cluster_create_samples}

Have you created a cluster before and are just looking for quick example commands? Try these examples.
{: shortdesc}



<img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> **Classic clusters**:
*  Classic cluster, shared virtual machine:
   ```
   ibmcloud oc cluster create classic --name my_cluster --version 4.5_openshift --zone dal10 --flavor b3c.4x16 --hardware shared --workers 3 --public-vlan <public_VLAN_ID> --private-vlan <private_VLAN_ID>
   ```
   {: pre}
*  Classic cluster, bare metal:
   ```
   ibmcloud oc cluster create classic --name my_cluster --version 4.5_openshift --zone dal10 --flavor mb2c.4x32 --hardware dedicated --workers 3 --public-vlan <public_VLAN_ID> --private-vlan <private_VLAN_ID>
   ```
   {: pre}
*  Classic cluster with an IBM Cloud&trade; Pak entitlement for a default worker pool of 3 worker nodes with 4 cores and 16 memory each:
   ```
   ibmcloud oc cluster create classic --name cloud_pak_cluster --version 4.5_openshift --zone dal10 --flavor b3c.4x16 --hardware dedicated --workers 3 --entitlement cloud_pak --public-vlan <public_VLAN_ID> --private-vlan <private_VLAN_ID>
   ```
   {: pre}
*  For a classic multizone cluster, after you created the cluster in a [multizone metro](/docs/openshift?topic=openshift-regions-and-zones#zones-mz), [add zones](/docs/openshift?topic=openshift-add_workers#add_zone):
   ```
   ibmcloud oc zone add classic --zone <zone> --cluster <cluster_name_or_ID> --worker-pool <pool_name> --private-vlan <private_VLAN_ID> --public-vlan <public_VLAN_ID>
   ```
   {: pre}



<img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> **VPC clusters**:
*  <img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC cluster:
    ```
    ibmcloud oc cluster create vpc-gen2 --name my_cluster --version 4.5_openshift --zone us-east-1 --vpc-id <VPC_ID> --subnet-id <VPC_SUBNET_ID> --cos-instance <COS_CRN>--flavor b2.4x16 --workers 3
    ```
    {: pre}
*  For a VPC multizone cluster, after you created the cluster in a [multizone metro](/docs/openshift?topic=openshift-regions-and-zones#zones-vpc), [add zones](/docs/openshift?topic=openshift-add_workers#vpc_add_zone):
   ```
   ibmcloud oc zone add vpc-gen2 --zone <zone> --cluster <cluster_name_or_ID> --worker-pool <pool_name> --subnet-id <VPC_SUBNET_ID>
   ```
   {: pre}


<br />

## Preparing to create clusters at the account level
{: #cluster_prepare}

Prepare your {{site.data.keyword.cloud_notm}} account for {{site.data.keyword.containerlong_notm}}. After the account administrator makes these preparations, you might not need to change them each time that you create a cluster. However, each time that you create a cluster, you still want to verify that the current account-level state is what you need it to be.
{: shortdesc}

1. [Create or upgrade your account to a billable account ({{site.data.keyword.cloud_notm}} Pay-As-You-Go or Subscription)](https://cloud.ibm.com/registration).

2. [Set up an API key for {{site.data.keyword.openshiftlong_notm}}](/docs/openshift?topic=openshift-users#api_key) in the region and resource groups where you want to create clusters. Assign the API key with the [required service and infrastructure permissions to create clusters](/docs/openshift?topic=openshift-access_reference#cluster_create_permissions).<p class="tip">Are you the account owner? You already have the necessary permissions! When you create a cluster, the API key for that region and resource group is set with your credentials.</p>

3. Verify that you as a user (not just the API key) have the required permissions to create clusters.
  1. From the [{{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/){: external} menu bar, click **Manage > Access (IAM)**.
  2. Click the **Users** page, and then from the table, select yourself.
  3. From the **Access policies** tab, confirm that you [have the required permissions to create clusters](/docs/openshift?topic=openshift-access_reference#cluster_create_permissions).
  <p class="tip">Make sure that your account administrator does not assign you the **Administrator** platform access role at the same time as scoping the access policy to a namespace.</p>

4. If your account uses multiple resource groups, figure out your account's strategy for [managing resource groups](/docs/openshift?topic=openshift-users#resource_groups).
  * The cluster is created in the resource group that you target when you log in to {{site.data.keyword.cloud_notm}}. If you do not target a resource group, the default resource group is automatically targeted. Free clusters are created in the `default` resource group.
  * If you want to create a cluster in a different resource group than the default, you need at least the **Viewer** role for the resource group. If you do not have any role for the resource group, your cluster is created in the default resource group.
  * You cannot change a cluster's resource group.
  * If you need to use the `ibmcloud oc cluster service bind` [command](/docs/containers-cli-plugin?topic=containers-cli-plugin-kubernetes-service-cli#cs_cluster_service_bind) to [integrate with an {{site.data.keyword.cloud_notm}} service](/docs/openshift?topic=openshift-service-binding#bind-services), that service must be in the same resource group as the cluster. Services that do not use resource groups like {{site.data.keyword.registrylong_notm}} or that do not need service binding like {{site.data.keyword.la_full_notm}} work even if the cluster is in a different resource group.
  * Consider giving clusters unique names across resource groups and regions in your account to avoid naming conflicts. You cannot rename a cluster.

4. <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> **Classic clusters only**: Consider [creating a reservation](/docs/openshift?topic=openshift-reservations) to lock in a discount over 1 or 3 year terms for your worker nodes. After you create the cluster, add worker pools that use the reserved instances. Typical savings range between 30-50% compared to on-demand worker node costs.

5. <img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> **VPC clusters only**: Set up your IBM Cloud infrastructure networking to allow worker-to-master and user-to-master communication. Your VPC clusters are created with a public and a private cloud service endpoint by default.
    1. Enable [VRF](/docs/account?topic=account-vrf-service-endpoint#vrf) in your IBM Cloud account.
    2. [Enable your {{site.data.keyword.cloud_notm}} account to use service endpoints](/docs/account?topic=account-vrf-service-endpoint#service-endpoint).
    3. Optional: If you want your VPC clusters to communicate with classic clusters over the private network interface, you can choose to set up classic infrastructure access from the VPC that your cluster is in. Note that you can set up classic infrastructure access for only one VPC per region and [Virtual Routing and Forwarding (VRF)](/docs/account?topic=account-vrf-service-endpoint#vrf) is required in your {{site.data.keyword.cloud_notm}} account. For more information, see [Setting up access to your Classic Infrastructure from VPC](/docs/vpc?topic=vpc-setting-up-access-to-classic-infrastructure).

<br />

## Deciding on your cluster setup
{: #prepare_cluster_level}
{: help}
{: support}

After you set up your account to create clusters, decide on the setup for your cluster. You must make these decisions every time that you create a cluster. You can click on the options in the following decision tree image for more information, such as comparisons of free and standard, Kubernetes and {{site.data.keyword.openshiftshort}}, or VPC and classic clusters.
{: shortdesc}

<p class="note">{{site.data.keyword.openshiftshort}} clusters are available only as standard clusters. You cannot get a [free](/docs/openshift?topic=openshift-faqs#faq_free) {{site.data.keyword.openshiftshort}} cluster.</p>

The following image walks you through choosing the setup that you want for your cluster.


<img usemap="#cluster-plan-map" border="0" class="image" src="images/cluster-plan-dt-vpc.png" alt="This image walks you through choosing the setup that you want for your cluster."/>
<map name="cluster-plan-map">
    <area target="" alt="Free and standard cluster comparison" title="Free and standard cluster comparison" href="/docs/containers?topic=containers-cs_ov#cluster_types" coords="43,9,361,106" shape="rect">
    <area target="" alt="OpenShift and Kubernetes comparison" title="OpenShift and Kubernetes comparison" href="/docs/openshift?topic=openshift-cs_ov#openshift_kubernetes" coords="110,128,467,224" shape="rect">
    <area target="" alt="VPC and classic infrastructure comparison" title="VPC and classic infrastructure comparison" href="/docs/containers?topic=containers-infrastructure_providers" coords="60,252,398,352" shape="rect">
    <area target="" alt="Locations" title="Locations" href="/docs/openshift?topic=openshift-regions-and-zones#zones-mz" coords="101,377,564,456" shape="rect">
    <area target="" alt="Virtual Machines" title="Virtual Machines" href="/docs/openshift?topic=openshift-planning_worker_nodes#vm" coords="105,488,564,538" shape="rect">
    <area target="" alt="Bare metal machines" title="Bare metal machines" href="/docs/openshift?topic=openshift-planning_worker_nodes#bm" coords="566,569,372,546" shape="rect">
    <area target="" alt="VPC scenarios" title="VPC scenarios" href="/docs/openshift?topic=openshift-plan_clusters#vpc-scenarios" coords="104,597,298,675" shape="rect">
    <area target="" alt="Classic scenarios" title="Classic scenarios" href="/docs/openshift?topic=openshift-plan_clusters#classic-scenarios" coords="369,596,566,674" shape="rect">
    <area target="" alt="Classic firewall" title="Classic firewall" href="/docs/containers?topic=containers-firewall" coords="369,681,564,704" shape="rect">
    <area target="" alt="VPC security groups and firewall" title="VPC security groups and firewall" href="/docs/containers?topic=containers-firewall" coords="103,680,298,704" shape="rect">
    <area target="" alt="Estimate costs (cluster create page)" title="Estimate costs (cluster create page)" href="https://cloud.ibm.com/kubernetes/catalog/create" coords="248,732,426,776" shape="rect">
</map>

<br />

## Creating a standard classic cluster
{: #clusters_standard}

<img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Use the {{site.data.keyword.cloud_notm}} CLI or the {{site.data.keyword.cloud_notm}} console to create a fully-customizable standard cluster with your choice of hardware isolation and access to features like multiple worker nodes for a highly available environment.
{: shortdesc}



### Creating a standard classic cluster in the console
{: #clusters_ui}

<img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Create your single zone or multizone classic {{site.data.keyword.openshiftshort}} cluster by using the {{site.data.keyword.cloud_notm}} console.
{: shortdesc}

1. Make sure that you complete the prerequisites to [prepare your account](#cluster_prepare) and decide on your [cluster setup](#prepare_cluster_level).
2. From the [{{site.data.keyword.openshiftshort}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, click **Create cluster**.
3. Configure your cluster environment.
   2. From the {{site.data.keyword.openshiftshort}} drop-down list, select the version that you want to use in your cluster, such as 4.5.35.
   3. **Optional**: For the **OCP entitlement** section, you can select an entitlement for a worker pool, if you have one. In most cases, leave the value set to **Purchase additional licenses for this worker pool**. If you have an {{site.data.keyword.cloud_notm}} Pak with an {{site.data.keyword.openshiftshort}} entitlement that you want to use, you can select **Apply my Cloud Pak OCP entitlement to this worker pool**. Later, when you configure the worker pool, make sure to select only the flavor and number of worker nodes that your entitlement permits.
4. Configure the **Location** details for your cluster.
   1. Select the **Resource group** that you want to create your cluster in.
      * A cluster can be created in only one resource group, and after the cluster is created, you cannot change its resource group.
      * To create clusters in a resource group other than the default, you must have at least the [**Viewer** role](/docs/openshift?topic=openshift-users#platform) for the resource group.
   2.  Select a **Geography** to create the cluster in, such as **North America**. The geography helps filter the **Availability** and **Metro** values that you can select.
   3.  Select the **Availability** that you want for your cluster, **Single zone** or **Multizone**. In a multizone cluster, the {{site.data.keyword.openshiftshort}} master is deployed in a multizone-capable zone and three replicas of your master are spread across zones.
   4. Enter the **Metro** and **Worker zones** details, depending on the availability that you selected for your cluster.
      *  **Multizone clusters**:
         1. Select a **Metro** location. For the best performance, select the metro location that is physically closest to you. Your choices might be limited by geography.
         2. Select the specific **Worker zones** within the metro to host your cluster. You must select at least one zone but you can select as many as you like. If you select more than one zone, the worker nodes are spread across the zones that you choose which gives you higher availability. If you select only one zone, you can [add zones to your cluster](/docs/openshift?topic=openshift-add_workers#add_zone) after the cluster is created.
      * **Single zone clusters**: Select a **Worker zone** in which you want to host your cluster. For the best performance, select the data center that is physically closest to you. Your choices might be limited by geography.
   5. For each of the selected zones, choose your public and private VLANs. You can change the pre-selected VLANs by clicking the **Edit VLANs** pencil icon. The first time that you create a cluster in a zone, public and private VLANs are automatically created for you. Worker nodes communicate with each other by using the private VLAN, and can communicate with the {{site.data.keyword.openshiftshort}} master by using the public or the private VLAN. If you do not have a public or private VLAN in this zone, a public and a private VLAN are automatically created for you. You can use the same VLAN for multiple clusters.
5. Configure your **Worker pool** setup. Worker pools are groups of worker nodes that share the same configuration. You can always add more worker pools to your cluster later.
   1.  If you want a larger size for your worker nodes, click **Change flavor**. The flavor defines the amount of virtual CPU, memory, and disk space that is set up in each worker node and made available to the containers. Available bare metal and virtual machines types vary by the zone in which you deploy the cluster. For more information, see [Planning your worker node setup](/docs/openshift?topic=openshift-planning_worker_nodes). After you create your cluster, you can add different flavors by adding a worker pool to the cluster.
      * **Default**: The default flavor is **Virtual - shared, Ubuntu 18**, which comes with **4 vCPUs** of computing power and **16 GB** of memory. This virtual flavor is billed hourly. Other types of flavors include the following.
      * **Bare metal**: Bare metal servers are provisioned manually by IBM Cloud infrastructure after you order, and can take more than one business day to complete. Bare metal is best suited for high-performance applications that need more resources and host control. Be sure that you want to provision a bare metal machine. Because it is billed monthly, if you cancel it immediately after an order by mistake, you are still charged the full month.
      * **Virtual - shared**: Infrastructure resources, such as the hypervisor and physical hardware, are shared across you and other IBM customers, but each worker node is accessible only by you. Although this option is less expensive and sufficient in most cases, you might want to verify your performance and infrastructure requirements with your company policies. Virtual machines are billed hourly.
      * **Virtual - dedicated**: Your worker nodes are hosted on infrastructure that is devoted to your account. Your physical resources are completely isolated. Virtual machines are billed hourly.
   2. Set how many worker nodes to create per zone, such as **3**. For example, if you selected 2 zones and want to create 3 worker nodes, a total of 6 worker nodes are provisioned in your cluster with 3 worker nodes in each zone. You must set at least 2 worker nodes. For more information, see [What is the smallest size cluster that I can make?](/docs/openshift?topic=openshift-faqs#smallest_cluster).
   3. Toggle disk encryption. By default, [worker nodes feature AES 256-bit disk encryption](/docs/openshift?topic=openshift-security#workernodes).
6. Configure your cluster with a public only or both a public and a private cloud service endpoint by setting the **Master service endpoint**. For more information about what setup is required to run internet-facing apps, or to keep your cluster private, see [Planning your cluster network setup](/docs/containers?topic=containers-plan_clusters#vpc-pgw). After you create the cluster, you cannot later change the cloud service endpoints.
7. If you do not have the required infrastructure permissions to create a cluster, the **Infrastructure permissions checker** lists the missing permissions. Ask your account owner to [set up the API key](/docs/openshift?topic=openshift-users#api_key) with the required permissions.

8. Complete the **Resource details** to customize the unique cluster name and any [tags](/docs/account?topic=account-tag) that you want to use to organize your {{site.data.keyword.cloud_notm}} resources, such as the team or billing department.

9. In the **Summary** pane, review your order summary and then click **Create**. A worker pool is created with the number of workers that you specified. You can see the progress of the worker node deployment in the **Worker nodes** tab.
   *  Your cluster might take some time to provision the {{site.data.keyword.openshiftshort}} master and all worker nodes and enter a   **Normal** state. Note that even if the cluster is ready, some parts of the cluster that are used by other services, such as Ingress  secrets or registry image pull secrets, might still be in process. Before you continue, wait until the cluster is ready by checking that the **Ingress subdomain** follows a pattern of `<cluster_name>.<region>.containers.appdomain.cloud`.
   *  Every worker node is assigned a unique worker node ID and domain name that must not be changed manually after the cluster is created. Changing the ID or domain name prevents the {{site.data.keyword.openshiftshort}} master from managing your cluster.<p class="tip">Is your cluster not in a **Normal** state? Check out the [Debugging clusters](/docs/openshift?topic=openshift-cs_troubleshoot) guide for help. For example, if your cluster is provisioned in an account that is protected by a firewall gateway appliance, you must [configure your firewall settings to allow outgoing traffic to the appropriate ports and IP addresses](/docs/openshift?topic=openshift-firewall#firewall_outbound).</p>
10. After your cluster is created, you can [begin working with your cluster by configuring your CLI session](/docs/openshift?topic=openshift-access_cluster). For more possibilities, review the [Next steps](/docs/openshift?topic=openshift-clusters#next_steps).

<br />

### Creating a standard classic cluster in the CLI
{: #clusters_cli_steps}

<img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Create your single zone or multizone classic cluster by using the {{site.data.keyword.cloud_notm}} CLI.
{: shortdesc}

**Before you begin**:
* Ensure that you complete the prerequisites to [prepare your account](#cluster_prepare) and decide on your [cluster setup](#prepare_cluster_level). Keep in mind that you need a cluster with a minimum of 2 worker nodes of the `4x16` flavor so that default {{site.data.keyword.openshiftshort}} components can deploy.
* Install the {{site.data.keyword.cloud_notm}} CLI and the [{{site.data.keyword.openshiftlong_notm}} plug-in](/docs/openshift?topic=openshift-openshift-cli).

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

3. Review the zones where you can create your cluster. In the output of the following command, zones have a **Location Type** of `dc`. To span your cluster across zones, you must create the cluster in a [multizone-capable zone](/docs/openshift?topic=openshift-regions-and-zones#zones-mz). Multizone-capable zones have a metro value in the **Multizone Metro** column. If you want to create a multizone cluster, you can use the {{site.data.keyword.cloud_notm}} console, or [add more zones](/docs/openshift?topic=openshift-add_workers#add_zone) to your cluster after the cluster is created.
    ```
    ibmcloud oc locations
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
   If a public and private VLAN already exist, note the matching routers. Private VLAN routers always begin with <code>bcr</code> (back-end router) and public VLAN routers always begin with <code>fcr</code> (front-end router). When you create a cluster and specify the public and private VLANs, the number and letter combination after those prefixes must match. In the example output, any private VLAN can be used with any public VLAN because the routers all include `02a.dal10`.

6. Create your standard cluster.
    ```
    ibmcloud oc cluster create classic --zone <zone> --flavor <flavor> --hardware <shared_or_dedicated> --public-vlan <public_VLAN_ID> --private-vlan <private_VLAN_ID> --workers <number> --name <cluster_name> --version <major.minor.patch>_openshift --public-service-endpoint [--private-service-endpoint] [--pod-subnet] [--service-subnet] [--disable-disk-encrypt]
    ```
    {: pre}

   <table summary="The columns are read from left to right. The first column has the parameter of the command. The second column describes the parameter.">
   <caption>`cluster create classic` command components</caption>
   <col width="25%">
   <thead>
   <th>Parameter</th>
   <th>Description</th>
   </thead>
   <tbody>
   <tr>
   <td><code>--zone <em>&lt;zone&gt;</em></code></td>
   <td>Specify the {{site.data.keyword.cloud_notm}} zone ID that you chose earlier and that you want to use to create your cluster.</td>
   </tr>
   <tr>
   <td><code>--flavor <em>&lt;flavor&gt;</em></code></td>
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
   <td><code>--name <em>&lt;name&gt;</em></code></td>
   <td>Specify a name for your cluster. The name must start with a letter, can contain letters, numbers, periods (.), and hyphen (-), and must be 35 characters or fewer. Use a name that is unique across regions. The cluster name and the region in which the cluster is deployed form the fully qualified domain name for the Ingress subdomain. To ensure that the Ingress subdomain is unique within a region, the cluster name might be truncated and appended with a random value within the Ingress domain name.</td>
   </tr>
   <tr>
   <td><code>--workers <em>&lt;number&gt;</em></code></td>
   <td>Specify the number of worker nodes to include in the cluster. If you do not specify this option, a cluster with the minimum value of 2 is created. For more information, see [What is the smallest size cluster that I can make?](/docs/openshift?topic=openshift-faqs#smallest_cluster).</td>
   </tr>
   <tr>
   <td><code>--version <em>&lt;major.minor.patch&gt;</em></code></td>
   <td>The {{site.data.keyword.openshiftshort}} version for the cluster master node. This value is required. When the version is not specified, the cluster is created with the default supported Kubernetes version. If you do not specify a supported {{site.data.keyword.openshiftshort}} version, your cluster is created as a community Kubernetes cluster. To see available versions, run <code>ibmcloud oc versions</code>.</td>
   </tr>
   <tr>
   <td><code>--public-service-endpoint</code></td>
   <td>Enable the public cloud service endpoint so that your {{site.data.keyword.openshiftshort}} master can be accessed over the public network, for example to run `oc` commands from your CLI, and so that your {{site.data.keyword.openshiftshort}} master and the worker nodes can communicate over the public VLAN. You must enable the public cloud service endpoint, and cannot later disable it.<br><br>After you create the cluster, you can get the endpoint by running `ibmcloud oc cluster get --cluster <cluster_name_or_ID>`.</td>
   </tr>
   <tr>
   <td><code>--private-service-endpoint</code></td>
   <td>**In [VRF-enabled](/docs/account?topic=account-vrf-service-endpoint#vrf) and [service endpoint-enabled](/docs/account?topic=account-vrf-service-endpoint#service-endpoint) accounts**: Enable the private cloud service endpoint so that your {{site.data.keyword.openshiftshort}} master and the worker nodes can communicate over the private VLAN. If you specify this flag, you must also enable the public cloud service endpoint by using the `--public-service-endpoint` flag. Note that you cannot later change the cloud service endpoints.<br><br>After you create the cluster, you can get the endpoint by running `ibmcloud oc cluster get --cluster <cluster_name_or_ID>`.</td>
   </tr>
   <tr>
   <td><code>--pod-subnet</code></td>
   <td>All pods that are deployed to a worker node are assigned a private IP address in the 172.30.0.0/16 range by default. If you plan to connect your cluster to on-premises networks through {{site.data.keyword.BluDirectLink}} or a VPN service, you can avoid subnet conflicts by specifying a custom subnet CIDR that provides the private IP addresses for your pods.
   <p>When you choose a subnet size, consider the size of the cluster that you plan to create and the number of worker nodes that you might add in the future. The subnet must have a CIDR of at least <code>/23</code>, which provides enough pod IPs for a maximum of four worker nodes in a cluster. For larger clusters, use <code>/22</code> to have enough pod IP addresses for eight worker nodes, <code>/21</code> to have enough pod IP addresses for 16 worker nodes, and so on.</p>
   <p>The subnet that you choose must be within one of the following ranges:
   <ul><li><code>172.17.0.0 - 172.17.255.255</code></li>
   <li><code>172.21.0.0 - 172.31.255.255</code></li>
   <li><code>192.168.0.0 - 192.168.254.255</code></li>
   <li><code>198.18.0.0 - 198.19.255.255</code></li></ul>Note that the pod and service subnets cannot overlap. The service subnet is in the 172.21.0.0/16 range by default.</p></td>
   </tr>
   <tr>
   <td><code>--service-subnet</code></td>
   <td>All services that are deployed to the cluster are assigned a private IP address in the 172.21.0.0/16 range by default. If you plan to connect your cluster to on-premises networks through {{site.data.keyword.dl_full_notm}} or a VPN service, you can avoid subnet conflicts by specifying a custom subnet CIDR that provides the private IP addresses for your services.
   <p>The subnet must be specified in CIDR format with a size of at least <code>/24</code>, which allows a maximum of 255 services in the cluster, or larger. The subnet that you choose must be within one of the following ranges:
   <ul><li><code>172.17.0.0 - 172.17.255.255</code></li>
   <li><code>172.21.0.0 - 172.31.255.255</code></li>
   <li><code>192.168.0.0 - 192.168.254.255</code></li>
   <li><code>198.18.0.0 - 198.19.255.255</code></li></ul>Note that the pod and service subnets cannot overlap. The pod subnet is in the 172.30.0.0/16 range by default.</p></td>
   </tr>
   <tr>
   <td><code>--disable-disk-encrypt</code></td>
   <td>Worker nodes feature AES 256-bit [disk encryption](/docs/openshift?topic=openshift-security#encrypted_disk) by default. If you want to disable encryption, include this option.</td>
   </tr>
   <tr>
   <td><code><strong>--entitlement cloud_pak</strong></code></td>
   <td>Include this flag only if you use this cluster with an [IBM Cloud Pak&trade;](/docs/openshift?topic=openshift-openshift_cloud_paks) that has an {{site.data.keyword.openshiftshort}} entitlement. When you specify the number of workers (`--workers`) and flavor (`--flavor`), make sure to specify only the number and size of worker nodes that you are entitled to use in [IBM Passport Advantage](https://www.ibm.com/software/passportadvantage/index.html){: external}. After your cluster is created, you are not charged the {{site.data.keyword.openshiftshort}} license fee for the entitled worker nodes in the `default` worker pool.<p class="important">Do not exceed your entitlement. Keep in mind that your OpenShift Container Platform entitlements can be used with other cloud providers or in other environments. To avoid billing issues later, make sure that you use only what you are entitled to use. For example, you might have an entitlement for the OCP licenses for two worker nodes of 4 CPU and 16 GB memory, and you create this worker pool with two worker nodes of 4 CPU and 16 GB memory. You used your entire entitlement, and you cannot use the same entitlement for other worker pools, cloud providers, or environments.</p></td></tr>
   </tbody></table>

7. Verify that the creation of the cluster was requested. For virtual machines, it can take a few minutes for the worker node machines to be ordered, and for the cluster to be set up and provisioned in your account. Bare metal physical machines are provisioned by manual interaction with IBM Cloud infrastructure, and can take more than one business day to complete.
   ```
   ibmcloud oc cluster ls
   ```
   {: pre}

   When the provisioning of your {{site.data.keyword.openshiftshort}} master is completed, the **State** of your cluster changes to `deployed`. After your {{site.data.keyword.openshiftshort}} master is ready, the provisioning of your worker nodes is initiated.
   ```
   Name         ID                         State      Created          Workers    Zone      Version     Resource Group Name   Provider
   mycluster    blrs3b1d0p0p2f7haq0g       deployed   20170201162433   3          dal10     4.5.35_xxxx_openshift      Default             classic
   ```
   {: screen}

   Is your cluster not in a `deployed` state? Check out the [Debugging clusters](/docs/openshift?topic=openshift-cs_troubleshoot) guide for help. For example, if your cluster is provisioned in an account that is protected by a firewall gateway appliance, you must [configure your firewall settings to allow outgoing traffic to the appropriate ports and IP addresses](/docs/openshift?topic=openshift-firewall#firewall_outbound).
   {: tip}

8. Check the status of the worker nodes.
   ```
   ibmcloud oc worker ls --cluster <cluster_name_or_ID>
   ```
   {: pre}

   When the worker nodes are ready, the worker node state changes to **normal** and the status changes to **Ready**. When the node status is **Ready**, you can then access the cluster. Note that even if the cluster is ready, some parts of the cluster that are used by other services, such as Ingress secrets or registry image pull secrets, might still be in process. Note that if you created your cluster with a private VLAN only, no **Public IP** addresses are assigned to your worker nodes.
   ```
   ID                                                     Public IP        Private IP     Flavor              State    Status   Zone    Version
   kube-blrs3b1d0p0p2f7haq0g-mycluster-default-000001f7   169.xx.xxx.xxx  10.xxx.xx.xxx   u3c.2x4.encrypted   normal   Ready    dal10   1.19.9
   ```
   {: screen}

   Every worker node is assigned a unique worker node ID and domain name that must not be changed manually after the cluster is created. Changing the ID or domain name prevents the {{site.data.keyword.openshiftshort}} master from managing your cluster.
   {: important}

9. **Optional**: If you created your cluster in a [multizone metro location](/docs/openshift?topic=openshift-regions-and-zones#zones-mz), you can [spread the default worker pool across zones](/docs/openshift?topic=openshift-add_workers#add_zone) to increase the cluster's availability.

10. After your cluster is created, you can [begin working with your cluster by configuring your CLI session](/docs/openshift?topic=openshift-access_cluster).

Your cluster is ready for your workloads! You might also want to [add a tag to your cluster](/docs/openshift?topic=openshift-add_workers#cluster_tags), such as the team or billing department that uses the cluster, to help manage {{site.data.keyword.cloud_notm}} resources. For more ideas of what to do with your cluster, review the [Next steps](/docs/openshift?topic=openshift-clusters#next_steps).

<br />



<br />

## Creating a standard VPC cluster
{: #clusters_vpcg2}

<img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Use the {{site.data.keyword.cloud_notm}} CLI or the {{site.data.keyword.cloud_notm}} console to create a standard VPC cluster, and customize your cluster to meet the high availability and security requirements of your apps.
{: shortdesc}

### Creating a standard VPC cluster in the console
{: #clusters_vpcg2_ui}

<img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Create your single zone or multizone VPC cluster by using the {{site.data.keyword.cloud_notm}} console.
{: shortdesc}

Your VPC cluster is created with both a public and a private cloud service endpoint. Want to create a VPC cluster with no public cloud service endpoint and only a private cloud service endpoint? Create the cluster [in the CLI](#cluster_vpcg2_cli) instead, and include the `--disable-public-service-endpoint` flag.
{: tip}

1. Make sure that you complete the prerequisites to [prepare your account](#cluster_prepare) and decide on your [cluster setup](#prepare_cluster_level).
2. [Create a Virtual Private Cloud (VPC) on generation 2 compute](https://cloud.ibm.com/vpc/provision/vpc){: external} with a subnet that is located in the VPC zone where you want to create the cluster.
  * During the VPC creation, you can create one subnet only. Subnets are specific to a zone. If you want to create a multizone cluster, create the subnet in one of the multizone-capable zones that you want to use. Later, you manually create the subnets for the remaining zones that you want to include in your cluster.<p class="important">Do not delete the subnets that you attach to your cluster during cluster creation or when you add worker nodes in a zone. If you delete a VPC subnet that your cluster used, any load balancers that use IP addresses from the subnet might experience issues, and you might be unable to create new load balancers.</p>
  * If worker nodes must access public endpoints, or if you plan to enable both the public and private cloud service endpoints, you must attach a public gateway to each subnet to access default {{site.data.keyword.openshiftshort}} components such as the web console or OperatorHub.
  * If you require access to classic infrastructure resources, you must follow the steps in [Creating VPC subnets for classic access](/docs/openshift?topic=openshift-vpc-subnets#ca_subnet_ui) to create a classic access VPC and VPC subnets without the automatic default address prefixes.
  * For more information, see [Creating a VPC using the IBM Cloud console](/docs/vpc?topic=vpc-creating-a-vpc-using-the-ibm-cloud-console) and [Overview of VPC networking in {{site.data.keyword.openshiftlong_notm}}: Subnets](/docs/openshift?topic=openshift-vpc-subnets#vpc_basics_subnets).
3. If you want to create a multizone cluster, create the subnets for all of the remaining zones that you want to include in your cluster. You must have one VPC subnet in all of the zones where you want to create your multizone cluster.
   1. From the [VPC subnet dashboard](https://cloud.ibm.com/vpc/network/subnets){: external}, click **New subnet**.
   3. Enter a name for your subnet and select the name of the VPC that you created.
   4. Select the location and zone where you want to create the subnet.
   5. Specify the number of IP addresses to create. VPC subnets provide IP addresses for your worker nodes and load balancer services in the cluster, so [create a VPC subnet with enough IP addresses](/docs/openshift?topic=openshift-vpc-subnets#vpc_basics_subnets), such as 256. You cannot change the number of IPs that a VPC subnet has later. If you enter a specific IP range, do not use the following reserved ranges: `172.16.0.0/16`, `172.18.0.0/16`, `172.19.0.0/16`, and `172.20.0.0/16`.
   6. Choose if you want to attach a public network gateway to your subnet. If you plan to enable both the public and private cloud service endpoints, you must attach a public gateway to each subnet to access default {{site.data.keyword.openshiftshort}} components such as the web console or OperatorHub. Additionally, a public network gateway is required when you want your cluster to access public endpoints, such as a public URL of another app or an {{site.data.keyword.cloud_notm}} service that supports public cloud service endpoints only. Make sure to review the [VPC networking basics](/docs/openshift?topic=openshift-plan_clusters#plan_vpc_basics) to understand when a public network gateway is required and how you can set up your cluster to limit public access to one or more subnets only.
   7. Click **Create subnet**.
4. From the [{{site.data.keyword.openshiftshort}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, click **Create cluster**.
5. Configure your cluster environment.
   1. Select the **Standard** cluster plan.
   2. From the {{site.data.keyword.openshiftshort}} drop-down list, select the version that you want to use in your cluster. You must choose **{{site.data.keyword.openshiftshort}} 4.4 or later**.
   3. **Optional**: For the **OCP entitlement** section, you can select an entitlement for a worker pool, if you have one. In most cases, leave the value set to **Purchase additional licenses for this worker pool**. If you have an {{site.data.keyword.cloud_notm}} Pak with an {{site.data.keyword.openshiftshort}} entitlement that you want to use, you can select **Apply my Cloud Pak OCP entitlement to this worker pool**. Later, when you configure the worker pool, make sure to select only the flavor and number of worker nodes that your entitlement permits.
   3. Select **VPC** infrastructure.
   4. From the **Virtual private cloud** drop-down menu, select the VPC that you created earlier.
   5.  From the **Cloud Object Storage** drop-down menu, select a standard {{site.data.keyword.cos_full_notm}} instance to use for the internal {{site.data.keyword.openshiftshort}} container registry, or [create a standard {{site.data.keyword.cos_full_notm}} instance](/docs/cloud-object-storage/basics?topic=cloud-object-storage-provision#provision-instance) to use.
6. Configure the **Location** details for your cluster.
   1. Select the **Resource group** that you want to create your cluster in.
      * A cluster can be created in only one resource group, and after the cluster is created, you cannot change its resource group.
      * To create clusters in a resource group other than the default, you must have at least the [**Viewer** role](/docs/openshift?topic=openshift-users#platform) for the resource group.
   2. Select the zones to create your cluster in.
      * The zones are filtered based on the VPC that you selected, and include the VPC subnets that you previously created.
      * To create a [single zone cluster](/docs/openshift?topic=openshift-ha_clusters#single_zone), select one zone only. If you select only one zone, you can [add zones to your cluster](/docs/openshift?topic=openshift-add_workers#add_zone) after the cluster is created.
      * To create a [multizone cluster](/docs/openshift?topic=openshift-ha_clusters#multizone), select multiple zones.
7. Configure your **Worker pool** setup. Worker pools are groups of worker nodes that share the same configuration. You can always add more worker pools to your cluster later.
   1.  If you want a larger size for your worker nodes, click **Change flavor**. The flavor defines the amount of virtual CPU, memory, and disk space that is set up in each worker node and made available to the containers. Available bare metal and virtual machines types vary by the zone in which you deploy the cluster. For more information, see [Planning your worker node setup](/docs/openshift?topic=openshift-planning_worker_nodes). After you create your cluster, you can add different flavors by adding a worker pool to the cluster.
      * **Default**: The default flavor is **Virtual - shared, Ubuntu 18**, which comes with **4 vCPUs** of computing power and **16 GB** of memory. This virtual flavor is billed hourly. Other types of flavors include the following.
      * **Bare metal**: Bare metal servers are provisioned manually by IBM Cloud infrastructure after you order, and can take more than one business day to complete. Bare metal is best suited for high-performance applications that need more resources and host control. Be sure that you want to provision a bare metal machine. Because it is billed monthly, if you cancel it immediately after an order by mistake, you are still charged the full month.
      * **Virtual - shared**: Infrastructure resources, such as the hypervisor and physical hardware, are shared across you and other IBM customers, but each worker node is accessible only by you. Although this option is less expensive and sufficient in most cases, you might want to verify your performance and infrastructure requirements with your company policies. Virtual machines are billed hourly.
      * **Virtual - dedicated**: Your worker nodes are hosted on infrastructure that is devoted to your account. Your physical resources are completely isolated. Virtual machines are billed hourly.
   2. Set how many worker nodes to create per zone, such as **3**. For example, if you selected 2 zones and want to create 3 worker nodes, a total of 6 worker nodes are provisioned in your cluster with 3 worker nodes in each zone. You must set at least 2 worker nodes. For more information, see [What is the smallest size cluster that I can make?](/docs/openshift?topic=openshift-faqs#smallest_cluster).
   3. Toggle disk encryption. By default, [worker nodes feature AES 256-bit disk encryption](/docs/openshift?topic=openshift-security#workernodes).
9. If you do not have the required infrastructure permissions to create a cluster, the **Infrastructure permissions checker** lists the missing permissions. Ask your account owner to [set up the API key](/docs/openshift?topic=openshift-users#api_key) with the required permissions.
10. Complete the **Resource details** to customize the unique cluster name and any [tags](/docs/account?topic=account-tag) that you want to use to organize your {{site.data.keyword.cloud_notm}} resources, such as the team or billing department.
11. In the **Summary** pane, review the order summary and then click **Create**. A worker pool is created with the number of workers that you specified. You can see the progress of the worker node deployment in the **Worker nodes** tab.
   *  Your cluster might take some time to provision the {{site.data.keyword.openshiftshort}} master and all worker nodes and enter a   **Normal** state. Note that even if the cluster is ready, some parts of the cluster that are used by other services, such as Ingress  secrets or registry image pull secrets, might still be in process. Before you continue, wait until the cluster is ready by checking that the **Ingress subdomain** follows a pattern of `<cluster_name>.<region>.containers.appdomain.cloud`.
   *  Every worker node is assigned a unique worker node ID and domain name that must not be changed manually after the cluster is created. Changing the ID or domain name prevents the {{site.data.keyword.openshiftshort}} master from managing your cluster.<p class="tip">Is your cluster not in a **Normal** state? Check out the [Debugging clusters](/docs/openshift?topic=openshift-cs_troubleshoot) guide for help. For example, if your cluster is provisioned in an account that is protected by a firewall gateway appliance, you must [configure your firewall settings to allow outgoing traffic to the appropriate ports and IP addresses](/docs/openshift?topic=openshift-firewall#firewall_outbound).</p>
12. After your cluster is created, you can [begin working with your cluster by configuring your CLI session](/docs/openshift?topic=openshift-access_cluster). For more possibilities, review the [Next steps](/docs/openshift?topic=openshift-clusters#next_steps).
13. {{site.data.keyword.openshiftshort}} version 4.4 or earlier only: To allow any traffic requests to apps that you deploy on your worker nodes, modify the VPC's default security group.
 1. From the [Virtual private cloud dashboard](https://cloud.ibm.com/vpc-ext/network/vpcs){: external}, click the name of the **Default Security Group** for the VPC that you created.
 2. In the **Inbound rules** section, click **New rule**.
 3. Choose the **TCP** protocol, enter `30000` for the **Port min** and `32767` for the **Port max**, and leave the **Any** source type selected.
 4. Click **Save**.
 5. If you require VPC VPN access or classic infrastructure access into this cluster, repeat these steps to add a rule that uses the **UDP** protocol, `30000` for the **Port min**, `32767` for the **Port max**, and the **Any** source type.

### Creating standard VPC clusters from the CLI
{: #cluster_vpcg2_cli}

<img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Create your single zone or multizone VPC cluster by using the {{site.data.keyword.cloud_notm}} CLI.
{: shortdesc}

**Before you begin**:
* Make sure that you complete the prerequisites to [prepare your account](#cluster_prepare) and decide on your [cluster setup](#prepare_cluster_level).
* Install the {{site.data.keyword.cloud_notm}} CLI and the [{{site.data.keyword.openshiftlong_notm}} plug-in](/docs/containers?topic=containers-cs_cli_install#cs_cli_install).
* Install the [VPC CLI plug-in](/docs/vpc?topic=vpc-infrastructure-cli-plugin-vpc-reference#cli-ref-prereqs).

<br>

**To create a VPC cluster from the CLI**:

1. In your command line, log in to your {{site.data.keyword.cloud_notm}} account and target the {{site.data.keyword.cloud_notm}} region and resource group where you want to create your VPC cluster. For supported regions, see [Creating a VPC in a different region](/docs/vpc?topic=vpc-creating-a-vpc-in-a-different-region). Enter your {{site.data.keyword.cloud_notm}} credentials when prompted. If you have a federated ID, use the --sso flag to log in.
   ```
   ibmcloud login -r <region> [-g <resource_group>] [--sso]
   ```
   {: pre}

3. [Create a VPC](/docs/vpc?topic=vpc-creating-a-vpc-using-cli#create-a-vpc-cli) in the same region where you want to create the cluster.<p class="important">Do the clusters of worker nodes in your VPC need to send and receive information to and from IBM Cloud classic infrastructure? Follow the steps in [Creating VPC subnets for classic access](/docs/openshift?topic=openshift-vpc-subnets#ca_subnet_cli) to create a classic-enabled VPC and VPC subnets without the automatic default address prefixes.<p>
4. [Create a subnet for your VPC](/docs/vpc?topic=vpc-creating-a-vpc-using-cli#create-a-subnet-cli).
  * If you want to create a [multizone cluster](/docs/openshift?topic=openshift-ha_clusters#multizone), repeat this step to create additional subnets in all of the zones that you want to include in your cluster.
  * VPC subnets provide IP addresses for your worker nodes and load balancer services in the cluster, so [create a VPC subnet with enough IP addresses](/docs/openshift?topic=openshift-vpc-subnets#vpc_basics_subnets), such as 256. You cannot change the number of IPs that a VPC subnet has later.
  * Do not use the following reserved ranges: `172.16.0.0/16`, `172.18.0.0/16`, `172.19.0.0/16`, and `172.20.0.0/16`.
  * If worker nodes must access public endpoints, or if you plan to enable both the public and private cloud service endpoints, you must [attach a public gateway](/docs/vpc?topic=vpc-creating-a-vpc-using-cli#attach-public-gateway-cli) to each subnet to access default {{site.data.keyword.openshiftshort}} components such as the web console or OperatorHub.
  * **Important**: Do not delete the subnets that you attach to your cluster during cluster creation or when you add worker nodes in a zone. If you delete a VPC subnet that your cluster used, any load balancers that use IP addresses from the subnet might experience issues, and you might be unable to create new load balancers.
  * For more information, see [Overview of VPC networking in {{site.data.keyword.openshiftlong_notm}}: Subnets](/docs/openshift?topic=openshift-vpc-subnets#vpc_basics_subnets).
5. Create the cluster in your VPC. You can use the `ibmcloud oc cluster create vpc-gen2` command to create a single zone cluster in your VPC with worker nodes that are connected to one VPC subnet only. If you want to create a multizone cluster, you can use the {{site.data.keyword.cloud_notm}} console, or [add more zones](/docs/openshift?topic=openshift-add_workers#vpc_add_zone) to your cluster after the cluster is created. The cluster takes a few minutes to provision.
    ```
    ibmcloud oc cluster create vpc-gen2 --name <cluster_name> --zone <vpc_zone> --vpc-id <vpc_ID> --subnet-id <vpc_subnet_ID> --flavor <worker_flavor> --version 4.5_openshift --cos-instance <COS_CRN> [--workers <number_workers_per_zone>] [--pod-subnet] [--service-subnet] [--disable-public-service-endpoint]
    ```
    {: pre}

    <table summary="The columns are read from left to right. The first column has the parameter of the command. The second column describes the parameter.">
    <caption>Cluster create components</caption>
    <col width="25%">
    <thead>
    <th>Parameter</th>
    <th>Description</th>
    </thead>
    <tbody>
    <tr>
    <td><code>--name <em>&lt;cluster_name&gt;</em></code></td>
    <td>Specify a name for your cluster. The name must start with a letter, can contain letters, numbers, periods (.), and hyphen (-), and must be 35 characters or fewer. Use a name that is unique across regions. The cluster name and the region in which the cluster is deployed form the fully qualified domain name for the Ingress subdomain. To ensure that the Ingress subdomain is unique within a region, the cluster name might be truncated and appended with a random value within the Ingress domain name.</td>
    </tr>
    <tr>
    <td><code>--zone <em>&lt;zone&gt;</em></code></td>
    <td>Specify the {{site.data.keyword.cloud_notm}} zone where you want to create your cluster. Make sure that you use a zone that matches the metro city location that you selected when you created your VPC and that you have an existing VPC subnet for that zone. For example, if you created your VPC in the Dallas metro city, your zone must be set to <code>us-south-1</code>, <code>us-south-2</code>, or <code>us-south-3</code>. To list available VPC cluster zones, run <code>ibmcloud oc zone ls --provider vpc-gen2</code>. Note that when you select a zone outside of your country, you might require legal authorization before data can be physically stored in a foreign country.</td>
    </tr>
    <tr>
    <td><code>--vpc-id <em>&lt;vpc_ID&gt;</em></code></td>
    <td>Enter the ID of the VPC that you created earlier. To retrieve the ID of your VPC, run <code>ibmcloud oc vpcs</code>. </td>
    </tr>
    <tr>
    <td><code>--subnet-id <em>&lt;subnet_ID&gt;</em></code></td>
    <td>Enter the ID of the VPC subnet that you created earlier. When you create a VPC cluster from the CLI, you can initially create your cluster in one zone with one subnet only. To create a multizone cluster, [add more zones](/docs/openshift?topic=openshift-add_workers) with the subnets that you created earlier to your cluster after the cluster is created. To list the IDs of your subnets in all resource groups, run <code> ibmcloud oc subnets --provider vpc-gen2 --vpc-id &lt,VPC_ID&gt; --zone &lt;subnet_zone&gt; </code>.  </td>
    </tr>
    <tr>
    <td><code>--flavor <em>&lt;worker_flavor&gt;</em></code></td>
    <td>Enter the worker node flavor that you want to use. The flavor determines the amount of virtual CPU, memory, and disk space that is set up in each worker node and made available to your apps. VPC worker nodes can be created as virtual machines on shared infrastructure only. Bare metal or software-defined storage machines are not supported.  For more information, see [Planning your worker node setup](/docs/openshift?topic=openshift-planning_worker_nodes). To view available flavors, first list available VPC zones with <code>ibmcloud oc zone ls --provider vpc-gen2</code>, and then use the zone to list supported flavors by running <code>ibmcloud oc flavors --zone &lt;VPC_zone&gt; --provider vpc-gen2</code>. After you create your cluster, you can add different flavors by adding a worker node or worker pool to the cluster.</td>
    </tr>
    <tr>
    <td><code>--version 4.5_openshift</code></td>
    <td>VPC clusters are supported for {{site.data.keyword.openshiftshort}} version 4 only.</td>
    </tr>
    <tr>
    <td><code>--cos-instance <em>&lt;cos_CRN&gt;</em></code></td>
    <td>Include the CRN ID of a standard {{site.data.keyword.cos_full_notm}} instance to back up the internal registry of your cluster. To list the CRN of existing instances, run <code>ibmcloud resource service-instances --long</code> and find the **ID** of your object storage instance. To create a standard object storage instance, run <code>ibmcloud resource service-instance-create <name> cloud-object-storage standard global</code> and note its **ID**.</td>
    </tr>
    <tr>
    <td><code>--workers <em>&lt;number&gt;</em></code></td>
    <td>Specify the number of worker nodes to include in the cluster. If you do not specify this option, a cluster with the minimum value of 2 is created. For more information, see [What is the smallest size cluster that I can make?](/docs/openshift?topic=openshift-faqs#smallest_cluster). This value is optional.</td>
    </tr>
    <tr>
    <td><code>--pod-subnet</code></td>
    <td>In the first cluster that you create in a VPC, the default pod subnet is `172.17.0.0/18`. In the second cluster that you create in that VPC, the default pod subnet is `172.17.64.0/18`. In each subsequent cluster, the pod subnet range is the next available, non-overlapping `/18` subnet. If you plan to connect your cluster to on-premises networks through {{site.data.keyword.BluDirectLink}} or a VPN service, you can avoid subnet conflicts by specifying a custom subnet CIDR that provides the private IP addresses for your pods.
    <p>When you choose a subnet size, consider the size of the cluster that you plan to create and the number of worker nodes that you might add in the future. The subnet must have a CIDR of at least <code>/23</code>, which provides enough pod IPs for a maximum of four worker nodes in a cluster. For larger clusters, use <code>/22</code> to have enough pod IP addresses for eight worker nodes, <code>/21</code> to have enough pod IP addresses for 16 worker nodes, and so on.</p>
    <p>The subnet that you choose must be within one of the following ranges:
    <ul><li><code>172.17.0.0 - 172.17.255.255</code></li>
    <li><code>172.21.0.0 - 172.31.255.255</code></li>
    <li><code>192.168.0.0 - 192.168.254.255</code></li>
    <li><code>198.18.0.0 - 198.19.255.255</code></li></ul>Note that the pod and service subnets cannot overlap. If you use custom-range subnets for your worker nodes, you must [ensure that your worker node subnets do not overlap with your cluster's pod subnet](/docs/openshift?topic=openshift-vpc-subnets#vpc-ip-range).</p></td>
    </tr>
    <tr>
    <td><code>--service-subnet</code></td>
    <td>All services that are deployed to the cluster are assigned a private IP address in the 172.21.0.0/16 range by default. If you plan to connect your cluster to on-premises networks through {{site.data.keyword.dl_full_notm}} or a VPN service, you can avoid subnet conflicts by specifying a custom subnet CIDR that provides the private IP addresses for your services.
    <p>The subnet must be specified in CIDR format with a size of at least <code>/24</code>, which allows a maximum of 255 services in the cluster, or larger. The subnet that you choose must be within one of the following ranges:
    <ul><li><code>172.17.0.0 - 172.17.255.255</code></li>
    <li><code>172.21.0.0 - 172.31.255.255</code></li>
    <li><code>192.168.0.0 - 192.168.254.255</code></li>
    <li><code>198.18.0.0 - 198.19.255.255</code></li></ul>Note that the pod and service subnets cannot overlap.</p></td>
    </tr>
    <tr>
    <td><code>--disable-public-service-endpoint</code></td>
    <td>Include this option in your command to create your VPC cluster with a private cloud service endpoint only. If you do not include this option, your cluster is set up with a public and a private cloud service endpoint. The service endpoint determines how your {{site.data.keyword.openshiftshort}} master and the worker nodes communicate, how your cluster access other {{site.data.keyword.cloud_notm}} services and apps outside the cluster, and how your users connect to your cluster. For more information, see [Planning your cluster network setup](/docs/openshift?topic=openshift-plan_clusters).<p class="important">If you include this flag, your cluster is created with routers and Ingress controllers that expose your apps on the private network only by default. If you later want to expose apps to a public network, you must manually create public routers and Ingress controllers.</p></td>
    </tr>
    </tbody></table>
6. Verify that the creation of the cluster was requested. It can take a few minutes for the worker node machines to be ordered, and for the cluster to be set up and provisioned in your account.
    ```
    ibmcloud oc cluster ls
    ```
    {: pre}

    When the provisioning of your {{site.data.keyword.openshiftshort}} master is completed, the status of your cluster changes to **deployed**. After the {{site.data.keyword.openshiftshort}} master is ready, your worker nodes are set up.
    ```
    Name         ID                                   State      Created          Workers    Zone      Version     Resource Group Name   Provider
    mycluster    aaf97a8843a29941b49a598f516da72101   deployed   20170201162433   3          mil01     1.19.9      Default               vpc-gen2
    ```
    {: screen}

    Is your cluster not in a **deployed** state? Check out the [Debugging clusters](/docs/openshift?topic=openshift-cs_troubleshoot) guide for help. For example, if your cluster is provisioned in an account that is protected by a firewall gateway appliance, you must [configure your firewall settings to allow outgoing traffic to the appropriate ports and IP addresses](/docs/openshift?topic=openshift-firewall#firewall_outbound).
    {: tip}

7. Check the status of the worker nodes.
   ```
   ibmcloud oc worker ls --cluster <cluster_name_or_ID>
   ```
   {: pre}

   When the worker nodes are ready, the worker node **State** changes to `deployed` and the **Status** changes to `Ready`. When the node **Status** changes to `Ready`, you can access the cluster. Note that even if the cluster is ready, some parts of the cluster that are used by other services, such as Ingress secrets or registry image pull secrets, might still be in process.
   ```
   ID                                                     Public IP        Private IP     Flavor              State    Status   Zone    Version
   kube-blrs3b1d0p0p2f7haq0g-mycluster-default-000001f7   169.xx.xxx.xxx  10.xxx.xx.xxx   u3c.2x4.encrypted   normal   Ready    dal10   1.19.9
   ```
   {: screen}

   Every worker node is assigned a unique worker node ID and domain name that must not be changed manually after the cluster is created. Changing the ID or domain name prevents the {{site.data.keyword.openshiftshort}} master from managing your cluster.
   {: important}

8. **Optional**: If you created your cluster in a [multizone metro location](/docs/openshift?topic=openshift-regions-and-zones#zones-vpc), you can [spread the default worker pool across zones](/docs/openshift?topic=openshift-add_workers#vpc_add_zone) to increase the cluster's availability.

9. After your cluster is created, you can [begin working with your cluster by configuring your CLI session](/docs/openshift?topic=openshift-access_cluster).

10. {{site.data.keyword.openshiftshort}} version 4.4 or earlier only: To allow any traffic requests to apps that you deploy on your worker nodes, modify the VPC's default security group.
    1. List your security groups. For the **VPC** that you created, note the ID of the default security group.
      ```
      ibmcloud is security-groups
      ```
      {: pre}
      Example output with only the default security group of a randomly generated name, `preppy-swimmer-island-green-refreshment`:
      ```
      ID                                     Name                                       Rules   Network interfaces         Created                     VPC                      Resource group
      1a111a1a-a111-11a1-a111-111111111111   preppy-swimmer-island-green-refreshment    4       -                          2019-08-12T13:24:45-04:00   <vpc_name>(bbbb222b-.)   c3c33cccc33c333ccc3c33cc3c333cc3
      ```
      {: screen}

    2. Add a security group rule to allow inbound TCP traffic on ports 30000-32767.
      ```
      ibmcloud is security-group-rule-add <security_group_ID> inbound tcp --port-min 30000 --port-max 32767
      ```
      {: pre}

    3. If you require VPC VPN access or classic infrastructure access into this cluster, add a security group rule to allow inbound UDP traffic on ports 30000-32767.
      ```
      ibmcloud is security-group-rule-add <security_group_ID> inbound udp --port-min 30000 --port-max 32767
      ```
      {: pre}

Your cluster is ready for your workloads! You might also want to [add a tag to your cluster](/docs/openshift?topic=openshift-add_workers#cluster_tags), such as the team or billing department that uses the cluster, to help manage {{site.data.keyword.cloud_notm}} resources. For more ideas of what to do with your cluster, review the [Next steps](/docs/openshift?topic=openshift-clusters#next_steps).

<br />

## Next steps
{: #next_steps}

When the cluster is up and running, you can check out the following cluster administration tasks:
- If you created the cluster in a multizone capable zone, [spread worker nodes by adding a zone to your cluster](/docs/openshift?topic=openshift-add_workers).
- [Deploy an app in your cluster.](/docs/containers?topic=containers-deploy_app#app_cli)
- [Set up your own private registry in {{site.data.keyword.cloud_notm}} to store and share Docker images with other users.](/docs/Registry?topic=Registry-getting-started)
- [Set up the cluster autoscaler](/docs/openshift?topic=openshift-ca#ca) to automatically add or remove worker nodes from your worker pools based on your workload resource requests.
- Control who can create pods in your cluster with [pod security policies](/docs/containers?topic=containers-psp).

Then, you can check out the following network configuration steps for your cluster setup:
* <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic clusters:
  * Isolate networking workloads to edge worker nodes [in classic clusters without a gateway](/docs/openshift?topic=openshift-edge).
  * Expose your apps with [public networking services](/docs/openshift?topic=openshift-cs_network_planning#openshift_routers) or [private networking services](/docs/openshift?topic=openshift-cs_network_planning#private_access).
  * Connect your cluster with services in private networks outside of your {{site.data.keyword.cloud_notm}} account by setting up [{{site.data.keyword.dl_full_notm}}](/docs/dl?topic=dl-get-started-with-ibm-cloud-dl) or the [strongSwan IPSec VPN service](/docs/openshift?topic=openshift-vpn).
  * Create Calico host network policies to isolate your cluster on the [public network](/docs/openshift?topic=openshift-network_policies#isolate_workers_public) and on the [private network](/docs/openshift?topic=openshift-network_policies#isolate_workers).
* <img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC clusters:
  * [Back up your internal image registry to {{site.data.keyword.cos_full_notm}}.](/docs/openshift?topic=openshift-registry#cos_image_registry)
  * Expose your apps with [public networking services](/docs/openshift?topic=openshift-cs_network_planning#openshift_routers) or [private networking services](/docs/openshift?topic=openshift-cs_network_planning#private_access).
  * Connect your cluster with services in private networks outside of your {{site.data.keyword.cloud_notm}} account or with resources in other VPCs by [setting up the {{site.data.keyword.vpc_short}} VPN](/docs/openshift?topic=openshift-vpc-vpnaas).
  * [Add rules to the security group for your worker nodes](/docs/openshift?topic=openshift-vpc-network-policy) to control ingress and egress traffic to your VPC subnets.




