---

copyright: 
  years: 2014, 2022
lastupdated: "2022-03-14"

keywords: openshift, clusters

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Creating clusters
{: #clusters}

Create a cluster in {{site.data.keyword.openshiftlong}}.
{: shortdesc}

After [getting started](/docs/containers?topic=containers-getting-started), you might want to create a cluster that is customized to your use case and different public and private cloud environments. Consider the following steps to create the right cluster each time.

1. [Prepare your account to create clusters](/docs/openshift?topic=openshift-clusters#cluster_prepare). This step includes creating a billable account, setting up an API key with infrastructure permissions, making sure that you have Administrator access in {{site.data.keyword.cloud_notm}} IAM, planning resource groups, and setting up account networking.
2. [Decide on your cluster setup](/docs/openshift?topic=openshift-clusters#prepare_cluster_level). This step includes planning cluster network and HA setup, estimating costs, and if applicable, allowing network traffic through a firewall.
3. Create your [VPC Gen2](#clusters_vpcg2) or [classic](#clusters_standard) cluster by following the steps in the {{site.data.keyword.cloud_notm}} console or CLI.

![Version 3.11 icon.](images/icon-version-311.png) {{site.data.keyword.redhat_openshift_notm}} version 3.11 is deprecated, and becomes unsupported on 6 June 2022 (date subject to change). Instead, you can create a version 4 cluster.
{: deprecated}



## Sample commands
{: #cluster_create_samples}

Have you created a cluster before and are just looking for quick example commands? Try these examples.
{: shortdesc}



Looking for a fast way to create a cluster from the UI? Try out [Automating cluster creation with {{site.data.keyword.bpfull_notm}} templates](/docs/openshift?topic=openshift-templates).
{: preview}



![Classic infrastructure provider icon.](images/icon-classic-2.svg) **Classic clusters**

Classic cluster, shared virtual machine

```sh
ibmcloud oc cluster create classic --name my_cluster --version 4.8_openshift --zone dal10 --flavor b3c.4x16 --hardware shared --workers 3 --public-vlan <public_VLAN_ID> --private-vlan <private_VLAN_ID>
```
{: pre}



Classic cluster, bare metal

```sh
ibmcloud oc cluster create classic --name my_cluster --version 4.8_openshift --zone dal10 --flavor mb2c.4x32 --hardware dedicated --workers 3 --public-vlan <public_VLAN_ID> --private-vlan <private_VLAN_ID>
```
{: pre}



Classic cluster with an IBM Cloud Pak entitlement for a default worker pool of 3 worker nodes with 4 cores and 16 memory each.

```sh
ibmcloud oc cluster create classic --name cloud_pak_cluster --version 4.8_openshift --zone dal10 --flavor b3c.4x16 --hardware dedicated --workers 3 --entitlement cloud_pak --public-vlan <public_VLAN_ID> --private-vlan <private_VLAN_ID>
```
{: pre}

For a classic multizone cluster, after you created the cluster in a [multizone metro](/docs/openshift?topic=openshift-regions-and-zones#zones-mz), [add zones](/docs/openshift?topic=openshift-add_workers#add_zone):
```sh
ibmcloud oc zone add classic --zone <zone> --cluster <cluster_name_or_ID> --worker-pool <pool_name> --private-vlan <private_VLAN_ID> --public-vlan <public_VLAN_ID>
```
{: pre}



![VPC infrastructure provider icon.](images/icon-vpc-2.svg) **VPC clusters**

VPC cluster.

```sh
ibmcloud oc cluster create vpc-gen2 --name my_cluster --version 4.8_openshift --zone us-east-1 --vpc-id <VPC_ID> --subnet-id <VPC_SUBNET_ID> --cos-instance <COS_CRN>--flavor b2.4x16 --workers 3
```
{: pre}

For a VPC multizone cluster, after you created the cluster in a [multizone metro](/docs/openshift?topic=openshift-regions-and-zones#zones-vpc), [add zones](/docs/openshift?topic=openshift-add_workers#vpc_add_zone).

```sh
ibmcloud oc zone add vpc-gen2 --zone <zone> --cluster <cluster_name_or_ID> --worker-pool <pool_name> --subnet-id <VPC_SUBNET_ID>
```
{: pre}



## Preparing to create clusters at the account level
{: #cluster_prepare}

Prepare your {{site.data.keyword.cloud_notm}} account for {{site.data.keyword.containerlong_notm}}. After the account administrator makes these preparations, you might not need to change them each time that you create a cluster. However, each time that you create a cluster, you still want to verify that the current account-level state is what you need it to be.
{: shortdesc}

1. [Create or upgrade your account to a billable account ({{site.data.keyword.cloud_notm}} Pay-As-You-Go or Subscription)](https://cloud.ibm.com/registration).

2. [Set up an API key for {{site.data.keyword.openshiftlong_notm}}](/docs/containers?topic=containers-access-creds) in the region and resource groups where you want to create clusters. Assign the API key with the [required service and infrastructure permissions to create clusters](/docs/openshift?topic=openshift-access_reference#cluster_create_permissions).
    Are you the account owner? You already have the necessary permissions! When you create a cluster, the API key for that region and resource group is set with your credentials.
    {: tip}

3. Verify that you as a user (not just the API key) have the required permissions to create clusters.
    1. From the [{{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/){: external} menu bar, click **Manage > Access (IAM)**.
    2. Click the **Users** page, and then from the table, select yourself.
    3. From the **Access policies** tab, confirm that you [have the required permissions to create clusters](/docs/openshift?topic=openshift-access_reference#cluster_create_permissions). Make sure that your account administrator does not assign you the **Administrator** platform access role at the same time as scoping the access policy to a namespace.

4. If your account uses multiple resource groups, figure out your account's strategy for [managing resource groups](/docs/openshift?topic=openshift-access-overview#resource_groups).
    * The cluster is created in the resource group that you target when you log in to {{site.data.keyword.cloud_notm}}. If you don't target a resource group, the default resource group is automatically targeted. Free clusters are created in the `default` resource group.
    * If you want to create a cluster in a different resource group than the default, you need at least the **Viewer** role for the resource group. If you don't have any role for the resource group, your cluster is created in the default resource group.
    * You can't change a cluster's resource group.
    * If you need to use the `ibmcloud oc cluster service bind` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_service_bind) to [integrate with an {{site.data.keyword.cloud_notm}} service](/docs/openshift?topic=openshift-service-binding#bind-services), that service must be in the same resource group as the cluster. Services that don't use resource groups like {{site.data.keyword.registrylong_notm}} or that don't need service binding like {{site.data.keyword.la_full_notm}} work even if the cluster is in a different resource group.
    * Consider giving clusters unique names across resource groups and regions in your account to avoid naming conflicts. You can't rename a cluster.

5. ![Classic infrastructure provider icon.](images/icon-classic-2.svg) **Classic clusters only**: Consider [creating a reservation](/docs/containers?topic=containers-reservations) to lock in a discount over 1 or 3 year terms for your worker nodes. After you create the cluster, add worker pools that use the reserved instances. Typical savings range between 30-50% compared to on-demand worker node costs.

6. ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) **VPC clusters only**: Set up your IBM Cloud infrastructure networking to allow worker-to-master and user-to-master communication. Your VPC clusters are created with a public and a private cloud service endpoint by default. **Optional**: If you want your VPC clusters to communicate with classic clusters over the private network interface, you can choose to set up classic infrastructure access from the VPC that your cluster is in. Note that you can set up classic infrastructure access for only one VPC per region and [Virtual Routing and Forwarding (VRF)](/docs/account?topic=account-vrf-service-endpoint#vrf) is required in your {{site.data.keyword.cloud_notm}} account. For more information, see [Setting up access to your Classic Infrastructure from VPC](/docs/vpc?topic=vpc-setting-up-access-to-classic-infrastructure).



## Deciding on your cluster setup
{: #prepare_cluster_level}
{: help}
{: support}

After you set up your account to create clusters, decide on the setup for your cluster. You must make these decisions every time that you create a cluster. You can click on the options in the following decision tree image for more information, such as comparisons of free and standard, Kubernetes and {{site.data.keyword.redhat_openshift_notm}}, or VPC and classic clusters.
{: shortdesc}



{{site.data.keyword.redhat_openshift_notm}} clusters are available only as standard clusters. You can't get a [free](/docs/openshift?topic=openshift-faqs#faq_free) {{site.data.keyword.redhat_openshift_notm}} cluster.
{: note}



The following image walks you through choosing the setup that you want for your cluster.


![Setting up your cluster](images/cluster-plan-dt-vpc.png "Setting up your cluster"){: caption="Figure 1. Setting up your cluster" caption-side="bottom"}




## Creating a standard classic cluster
{: #clusters_standard}

![Classic infrastructure provider icon.](images/icon-classic-2.svg) Use the {{site.data.keyword.cloud_notm}} CLI or the {{site.data.keyword.cloud_notm}} console to create a fully-customizable standard cluster with your choice of hardware isolation and access to features like multiple worker nodes for a highly available environment.
{: shortdesc}



### Creating a standard classic cluster in the console
{: #clusters_ui}

![Classic infrastructure provider icon.](images/icon-classic-2.svg) Create your single zone or multizone classic {{site.data.keyword.redhat_openshift_notm}} cluster by using the {{site.data.keyword.cloud_notm}} console.
{: shortdesc}

{{site.data.keyword.openshiftlong_notm}} clusters are created with a public only or both a public and private service endpoint. Public service endpoints can't be disabled, and therefore, you can't convert a public {{site.data.keyword.redhat_openshift_notm}} cluster to a private one. If you want your cluster to remain private, see [Planning your cluster network setup](/docs/containers?topic=containers-plan_vpc_basics#vpc-pgw).
{: important}

1. Make sure that you complete the prerequisites to [prepare your account](#cluster_prepare) and decide on your [cluster setup](#prepare_cluster_level).
2. From the [{{site.data.keyword.redhat_openshift_notm}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, click **Create cluster**.
3. Configure your cluster environment.
    2. From the {{site.data.keyword.redhat_openshift_notm}} drop-down list, select the version that you want to use in your cluster, such as 4.7.29.
    3. **Optional**: For the **OCP entitlement** section, you can select an entitlement for a worker pool, if you have one. Usually, leave the value set to **Purchase additional licenses for this worker pool**. If you have an {{site.data.keyword.cloud_notm}} Pak with an {{site.data.keyword.redhat_openshift_notm}} entitlement that you want to use, you can select **Apply my Cloud Pak OCP entitlement to this worker pool**. Later, when you configure the worker pool, make sure to select only the flavor and number of worker nodes that your entitlement permits.
4. Configure the **Location** details for your cluster.
    1. Select the **Resource group** that you want to create your cluster in.
        * A cluster can be created in only one resource group, and after the cluster is created, you can't change its resource group.
        * To create clusters in a resource group other than the default, you must have at least the [**Viewer** role](/docs/openshift?topic=openshift-users#checking-perms) for the resource group.
    2. Select a **Geography** to create the cluster in, such as **North America**. The geography helps filter the **Availability** and **Metro** values that you can select.
    3. Select the **Availability** that you want for your cluster, **Single zone** or **Multizone**. In a multizone cluster, the {{site.data.keyword.redhat_openshift_notm}} master is deployed in a multizone-capable zone and three replicas of your master are spread across zones.
    4. Enter the **Metro** and **Worker zones** details, depending on the availability that you selected for your cluster.
        - **Multizone clusters**:
            1. Select a **Metro** location. For the best performance, select the metro location that is physically closest to you. Your choices might be limited by geography.
            2. Select the specific **Worker zones** within the metro to host your cluster. You must select at least one zone but you can select as many as you like. If you select more than one zone, the worker nodes are spread across the zones that you choose which gives you higher availability. If you select only one zone, you can [add zones to your cluster](/docs/openshift?topic=openshift-add_workers#add_zone) after the cluster is created.
        - **Single zone clusters**: Select a **Worker zone** in which you want to host your cluster. For the best performance, select the data center that is physically closest to you. Your choices might be limited by geography.
    5. For each of the selected zones, choose your public and private VLANs. You can change the pre-selected VLANs by clicking the **Edit VLANs** pencil icon. The first time that you create a cluster in a zone, public and private VLANs are automatically created for you. Worker nodes communicate with each other by using the private VLAN, and can communicate with the {{site.data.keyword.redhat_openshift_notm}} master by using the public or the private VLAN. If you don't have a public or private VLAN in this zone, a public and a private VLAN are automatically created for you. You can use the same VLAN for multiple clusters.
5. Configure your **Worker pool** setup. Worker pools are groups of worker nodes that share the same configuration. You can always add more worker pools to your cluster later.
    1. If you want a larger size for your worker nodes, click **Change flavor**. The flavor defines the amount of virtual CPU, memory, and disk space that is set up in each worker node and made available to the containers. Available bare metal and virtual machines types vary by the zone in which you deploy the cluster. For more information, see [Planning your worker node setup](/docs/containers?topic=containers-planning_worker_nodes). After you create your cluster, you can add different flavors by adding a worker pool to the cluster.
        Default
        :   The default flavor is **Virtual - shared, Ubuntu 18**, which comes with **4 vCPUs** of computing power and **16 GB** of memory. This virtual flavor is billed hourly. Other types of flavors include the following.
        Bare metal
        :   Bare metal servers are provisioned manually by IBM Cloud infrastructure after you order, and can take more than one business day to complete. Bare metal is best suited for high-performance applications that need more resources and host control. Be sure that you want to provision a bare metal machine. Because it is billed monthly, if you cancel it immediately after an order by mistake, you are still charged the full month.
        Virtual - shared
        :   Infrastructure resources, such as the hypervisor and physical hardware, are shared across you and other IBM customers, but each worker node is accessible only by you. Although this option is less expensive and sufficient in most cases, you might want to verify your performance and infrastructure requirements with your company policies. Virtual machines are billed hourly.
        Virtual - dedicated
        :   Your worker nodes are hosted on infrastructure that is devoted to your account. Your physical resources are completely isolated. Virtual machines are billed hourly.
    2. Set how many worker nodes to create per zone, such as **3**. For example, if you selected 2 zones and want to create 3 worker nodes, a total of 6 worker nodes are provisioned in your cluster with 3 worker nodes in each zone. You must set at least 2 worker nodes. For more information, see [What is the smallest size cluster that I can make?](/docs/openshift?topic=openshift-faqs#smallest_cluster).
    3. Toggle disk encryption. By default, [worker nodes feature AES 256-bit disk encryption](/docs/openshift?topic=openshift-security#workernodes).
    
6. Configure your cluster with a public only or both a public and a private cloud service endpoint by setting the **Master service endpoint**. For more information about what setup is required to run internet-facing apps, or to keep your cluster private, see [Planning your cluster network setup](/docs/containers?topic=containers-plan_vpc_basics#vpc-pgw). After you create the cluster, you can't later change the cloud service endpoints.

7. If you don't have the required infrastructure permissions to create a cluster, the **Infrastructure permissions checker** lists the missing permissions. Ask your account owner to [set up the API key](/docs/containers?topic=containers-access-creds) with the required permissions.

8. Complete the **Resource details** to customize the unique cluster name and any [tags](/docs/account?topic=account-tag) that you want to use to organize your {{site.data.keyword.cloud_notm}} resources, such as the team or billing department.

9. In the **Summary** pane, review your order summary and then click **Create**. A worker pool is created with the number of workers that you specified. You can see the progress of the worker node deployment in the **Worker nodes** tab.
    - Your cluster might take some time to provision the {{site.data.keyword.redhat_openshift_notm}} master and all worker nodes and enter a   **Normal** state. Note that even if the cluster is ready, some parts of the cluster that are used by other services, such as Ingress  secrets or registry image pull secrets, might still be in process. Before you continue, wait until the cluster is ready by checking that the **Ingress subdomain** follows a pattern of `<cluster_name>.<region>.containers.appdomain.cloud`.
    - Every worker node is assigned a unique worker node ID and domain name that must not be changed manually after the cluster is created. Changing the ID or domain name prevents the {{site.data.keyword.redhat_openshift_notm}} master from managing your cluster.
        Is your cluster not in a **Normal** state? Check out the [Debugging clusters](/docs/containers?topic=containers-debug_clusters) guide for help. For example, if your cluster is provisioned in an account that is protected by a firewall gateway appliance, you must [configure your firewall settings to allow outgoing traffic to the appropriate ports and IP addresses](/docs/openshift?topic=openshift-firewall#firewall_outbound).
        {: tip}
        
10. After your cluster is created, you can [begin working with your cluster by configuring your CLI session](/docs/openshift?topic=openshift-access_cluster). For more possibilities, review the [Next steps](/docs/openshift?topic=openshift-clusters#next_steps).



### Creating a standard classic cluster in the CLI
{: #clusters_cli_steps}

![Classic infrastructure provider icon.](images/icon-classic-2.svg) Create your single zone or multizone classic cluster by using the {{site.data.keyword.cloud_notm}} CLI.
{: shortdesc}

**Before you begin**:
* Ensure that you complete the prerequisites to [prepare your account](#cluster_prepare) and decide on your [cluster setup](#prepare_cluster_level). Keep in mind that you need a cluster with a minimum of 2 worker nodes of the `4x16` flavor so that default {{site.data.keyword.redhat_openshift_notm}} components can deploy.
* Install the {{site.data.keyword.cloud_notm}} CLI and the [{{site.data.keyword.openshiftlong_notm}} plug-in](/docs/openshift?topic=openshift-openshift-cli).


**To create a classic cluster from the CLI**:

1. Log in to the {{site.data.keyword.cloud_notm}} CLI. Log in and enter your {{site.data.keyword.cloud_notm}} credentials when prompted. If you have a federated ID, use `ibmcloud login --sso` to log in to the {{site.data.keyword.cloud_notm}} CLI.

    ```sh
    ibmcloud login [--sso]
    ```
    {: pre}

2. If you have multiple {{site.data.keyword.cloud_notm}} accounts, select the account where you want to create your Kubernetes cluster.

3. To create clusters in a resource group other than default, target that resource group. A cluster can be created in only one resource group, and after the cluster is created, you can't change its resource group. You must have at least the [**Viewer** role](/docs/openshift?topic=openshift-users#checking-perms) for the resource group.

    ```sh
    ibmcloud target -g <resource_group_name>
    ```
    {: pre} 

5. Review the zones where you can create your cluster. In the output of the following command, zones have a **Location Type** of `dc`. To span your cluster across zones, you must create the cluster in a [multizone-capable zone](/docs/openshift?topic=openshift-regions-and-zones#zones-mz). Multizone-capable zones have a metro value in the **Multizone Metro** column. If you want to create a multizone cluster, you can use the {{site.data.keyword.cloud_notm}} console, or [add more zones](/docs/openshift?topic=openshift-add_workers#add_zone) to your cluster after the cluster is created.
    ```sh
    ibmcloud oc locations
    ```
    {: pre}

    When you select a zone that is located outside your country, keep in mind that you might require legal authorization before data can be physically stored in a foreign country.
    {: note}

6. Review the worker node flavors that are available in that zone. The flavor determines the amount of virtual CPU, memory, and disk space that is set up in each worker node and made available to your apps. Worker nodes in classic clusters can be created as virtual machines on shared or dedicated infrastructure, or as bare metal machines that are dedicated to you. For more information, see [Planning your worker node setup](/docs/containers?topic=containers-planning_worker_nodes). After you create your cluster, you can add different flavors by [adding a worker pool](/docs/openshift?topic=openshift-add_workers#add_pool).

    Before you create a bare metal machine, be sure that you want to provision one. Bare metal machines are billed monthly. If you order a bare metal machine by mistake, you are charged for the entire month, even if you cancel the machine immediately.  
    {: tip}

    ```sh
    ibmcloud oc flavors --zone <zone>
    ```
    {: pre}

7. Check if you have existing VLANs in the zones that you want to include in your cluster, and note the ID of the VLAN. If you don't have a public or private VLAN in one of the zones that you want to use in your cluster, {{site.data.keyword.containerlong_notm}} automatically creates these VLANs for you when you create the cluster.
    ```sh
    ibmcloud oc vlan ls --zone <zone>
    ```
    {: pre}

    Example output

    ```sh
    ID        Name   Number   Type      Router
    1519999   vlan   1355     private   bcr02a.dal10
    1519898   vlan   1357     private   bcr02a.dal10
    1518787   vlan   1252     public    fcr02a.dal10
    1518888   vlan   1254     public    fcr02a.dal10
    ```
    {: screen}

    If a public and private VLAN already exist, note the matching routers. Private VLAN routers always begin with `bcr` (back-end router) and public VLAN routers always begin with `fcr` (front-end router). When you create a cluster and specify the public and private VLANs, the number and letter combination after those prefixes must match. In the example output, any private VLAN can be used with any public VLAN because the routers all include `02a.dal10`.

8. Create your standard cluster.
    ```sh
    ibmcloud oc cluster create classic --zone <zone> --flavor <flavor> --hardware <shared_or_dedicated> --public-vlan <public_VLAN_ID> --private-vlan <private_VLAN_ID> --workers <number> --name <cluster_name> --version <major.minor.patch>_openshift --public-service-endpoint [--private-service-endpoint] [--pod-subnet] [--service-subnet] [--disable-disk-encrypt]
    ```
    {: pre}

    `--zone <zone>`
    :   Specify the {{site.data.keyword.cloud_notm}} zone ID that you chose earlier and that you want to use to create your cluster.
    
    `--flavor <flavor>`
    :   Specify the flavor for your worker node that you chose earlier.
    
    `--hardware <shared_or_dedicated>`
    :   Specify with the level of hardware isolation for your worker node. Use `dedicated` to have available physical resources dedicated to you only, or `shared` to allow physical resources to be shared with other IBM customers. The default is shared. This value is optional for VM standard clusters. For bare metal flavors, specify `dedicated`.

    `--public-vlan <public_vlan_id>`
    :   If you already have a public VLAN set up in your IBM Cloud infrastructure account for that zone, enter the ID of the public VLAN that you retrieved earlier. If you don't have a public VLAN in your account, don't specify this option. {{site.data.keyword.containerlong_notm}} automatically creates a public VLAN for you. Private VLAN routers always begin with `bcr` (back-end router) and public VLAN routers always begin with `fcr` (front-end router). When you create a cluster and specify the public and private VLANs, the number and letter combination after those prefixes must match.

    `--private-vlan <private_vlan_id>`
    :   If you already have a private VLAN set up in your IBM Cloud infrastructure account for that zone, enter the ID of the private VLAN that you retrieved earlier. If you don't have a private VLAN in your account, don't specify this option. {{site.data.keyword.containerlong_notm}} automatically creates a private VLAN for you. Private VLAN routers always begin with `bcr` (back-end router) and public VLAN routers always begin with `fcr` (front-end router). When you create a cluster and specify the public and private VLANs, the number and letter combination after those prefixes must match.
    
    `--name <name>`
    :   Specify a name for your cluster. The name must start with a letter, can contain letters, numbers, periods (.), and hyphen (-), and must be 35 characters or fewer. Use a name that is unique across regions. The cluster name and the region in which the cluster is deployed form the fully qualified domain name for the Ingress subdomain. To ensure that the Ingress subdomain is unique within a region, the cluster name might be truncated and appended with a random value within the Ingress domain name.

    `--workers <number>`
    :   Specify at least 2 worker nodes to include in the cluster.  For more information, see [What is the smallest size cluster that I can make?](/docs/openshift?topic=openshift-faqs#smallest_cluster).

    `--version <major.minor.patch>`
    :   The {{site.data.keyword.redhat_openshift_notm}} version for the cluster master node. This value is required. When the version is not specified, the cluster is created with the default supported Kubernetes version. If you don't specify a supported {{site.data.keyword.redhat_openshift_notm}} version, your cluster is created as a community Kubernetes cluster. To see available versions, run `ibmcloud oc versions`.

    `--public-service-endpoint`
    :   Enable the public cloud service endpoint so that your {{site.data.keyword.redhat_openshift_notm}} master can be accessed over the public network, for example to run `oc` commands from your CLI, and so that your {{site.data.keyword.redhat_openshift_notm}} master and the worker nodes can communicate over the public VLAN. You must enable the public cloud service endpoint, and can't later disable it.After you create the cluster, you can get the endpoint by running `ibmcloud oc cluster get --cluster <cluster_name_or_ID>`.

    `--private-service-endpoint`
    :   In [VRF-enabled](/docs/account?topic=account-vrf-service-endpoint#vrf) and [service endpoint-enabled accounts](/docs/account?topic=account-vrf-service-endpoint#service-endpoint): Enable the private cloud service endpoint so that your {{site.data.keyword.redhat_openshift_notm}} master and the worker nodes can communicate over the private VLAN. If you specify this flag, you must also enable the public cloud service endpoint by using the `--public-service-endpoint` flag. Note that you can't later change the cloud service endpoints.After you create the cluster, you can get the endpoint by running `ibmcloud oc cluster get --cluster <cluster_name_or_ID>`.

    `--pod-subnet`
    :   All pods that are deployed to a worker node are assigned a private IP address in the 172.30.0.0/16 range by default. If you plan to connect your cluster to on-premises networks through {{site.data.keyword.BluDirectLink}} or a VPN service, you can avoid subnet conflicts by specifying a custom subnet CIDR that provides the private IP addresses for your pods.
    When you choose a subnet size, consider the size of the cluster that you plan to create and the number of worker nodes that you might add in the future. The subnet must have a CIDR of at least `/23`, which provides enough pod IPs for a maximum of four worker nodes in a cluster. For larger clusters, use `/22` to have enough pod IP addresses for eight worker nodes, `/21` to have enough pod IP addresses for 16 worker nodes, and so on. Note that the pod and service subnets can't overlap. The service subnet is in the 172.21.0.0/16 range by default.
    The subnet that you choose must be within one of the following ranges:
        - `172.17.0.0 - 172.17.255.255`
        - `172.21.0.0 - 172.31.255.255`
        - `192.168.0.0 - 192.168.254.255`
        - `198.18.0.0 - 198.19.255.255`
        

    `--service-subnet`
    :   All services that are deployed to the cluster are assigned a private IP address in the 172.21.0.0/16 range by default. If you plan to connect your cluster to on-premises networks through {{site.data.keyword.dl_full_notm}} or a VPN service, you can avoid subnet conflicts by specifying a custom subnet CIDR that provides the private IP addresses for your services.
    :   The subnet must be specified in CIDR format with a size of at least `/24`, which allows a maximum of 255 services in the cluster, or larger. The subnet that you choose must be within one of the following ranges:
        - `172.17.0.0 - 172.17.255.255`
        - `172.21.0.0 - 172.31.255.255`
        - `192.168.0.0 - 192.168.254.255`
        - `198.18.0.0 - 198.19.255.255`
        
    :   Note that the pod and service subnets can't overlap. The pod subnet is in the 172.30.0.0/16 range by default.

    `--disable-disk-encrypt`
    :   Worker nodes feature AES 256-bit [disk encryption by default](/docs/openshift?topic=openshift-security#encrypted_disk). If you want to disable encryption, include this option.
    
    `--entitlement cloud_pak`
    :   Include this flag only if you use this cluster with an [IBM Cloud Pak](/docs/openshift?topic=openshift-openshift_cloud_paks) that has an {{site.data.keyword.redhat_openshift_notm}} entitlement. When you specify the number of workers (`--workers`) and flavor (`--flavor`), make sure to specify only the number and size of worker nodes that you are entitled to use in [IBM Passport Advantage](https://www.ibm.com/software/passportadvantage/index.html){: external}. After your cluster is created, you are not charged the {{site.data.keyword.redhat_openshift_notm}} license fee for the entitled worker nodes in the `default` worker pool.
    Do not exceed your entitlement. Keep in mind that your OpenShift Container Platform entitlements can be used with other cloud providers or in other environments. To avoid billing issues later, make sure that you use only what you are entitled to use. For example, you might have an entitlement for the OCP licenses for two worker nodes of 4 CPU and 16 GB memory, and you create this worker pool with two worker nodes of 4 CPU and 16 GB memory. You used your entire entitlement, and you can't use the same entitlement for other worker pools, cloud providers, or environments.
    {: important}



9. Verify that the creation of the cluster was requested. For virtual machines, it can take a few minutes for the worker node machines to be ordered, and for the cluster to be set up and provisioned in your account. Bare metal physical machines are provisioned by manual interaction with IBM Cloud infrastructure, and can take more than one business day to complete.
    ```sh
    ibmcloud oc cluster ls
    ```
    {: pre}

    When the provisioning of your {{site.data.keyword.redhat_openshift_notm}} master is completed, the **State** of your cluster changes to `normal`. After your {{site.data.keyword.redhat_openshift_notm}} master is ready, the provisioning of your worker nodes is initiated.
    ```sh
    NAME         ID                         State      Created          Workers    Zone      Version     Resource Group Name   Provider
    mycluster    blrs3b1d0p0p2f7haq0g       normal   20170201162433   3          dal10     4.7.36_xxxx_openshift      Default             classic
    ```
    {: screen}

    Is your cluster not in a `normal` state? Check out the [Debugging clusters](/docs/containers?topic=containers-debug_clusters) guide for help. For example, if your cluster is provisioned in an account that is protected by a firewall gateway appliance, you must [configure your firewall settings to allow outgoing traffic to the appropriate ports and IP addresses](/docs/openshift?topic=openshift-firewall#firewall_outbound).
    {: tip}

10. Check the status of the worker nodes.
    ```sh
    ibmcloud oc worker ls --cluster <cluster_name_or_ID>
    ```
    {: pre}

    When the worker nodes are ready, the worker node state changes to **normal** and the status changes to **Ready**. When the node status is **Ready**, you can then access the cluster. Note that even if the cluster is ready, some parts of the cluster that are used by other services, such as Ingress secrets or registry image pull secrets, might still be in process. Note that if you created your cluster with a private VLAN only, no **Public IP** addresses are assigned to your worker nodes.
    ```sh
    ID                                                     Public IP        Private IP     Flavor              State    Status   Zone    Version
    kube-blrs3b1d0p0p2f7haq0g-mycluster-default-000001f7   169.xx.xxx.xxx  10.xxx.xx.xxx   u3c.2x4.encrypted   normal   Ready    dal10   1.22.7
    ```
    {: screen}

    Every worker node is assigned a unique worker node ID and domain name that must not be changed manually after the cluster is created. Changing the ID or domain name prevents the {{site.data.keyword.redhat_openshift_notm}} master from managing your cluster.
    {: important}

11. **Optional**: If you created your cluster in a [multizone metro location](/docs/openshift?topic=openshift-regions-and-zones#zones-mz), you can [spread the default worker pool across zones](/docs/openshift?topic=openshift-add_workers#add_zone) to increase the cluster's availability.

12. After your cluster is created, you can [begin working with your cluster by configuring your CLI session](/docs/openshift?topic=openshift-access_cluster).

Your cluster is ready for your workloads! You might also want to [add a tag to your cluster](/docs/openshift?topic=openshift-add_workers#cluster_tags), such as the team or billing department that uses the cluster, to help manage {{site.data.keyword.cloud_notm}} resources. For more ideas of what to do with your cluster, review the [Next steps](/docs/openshift?topic=openshift-clusters#next_steps).







## Creating a standard VPC cluster
{: #clusters_vpcg2}

![VPC infrastructure provider icon.](images/icon-vpc-2.svg) Use the {{site.data.keyword.cloud_notm}} CLI or the {{site.data.keyword.cloud_notm}} console to create a standard VPC cluster, and customize your cluster to meet the high availability and security requirements of your apps.
{: shortdesc}

### Creating a standard VPC cluster in the console
{: #clusters_vpcg2_ui}

![VPC infrastructure provider icon.](images/icon-vpc-2.svg) Create your single zone or multizone VPC cluster by using the {{site.data.keyword.cloud_notm}} console.
{: shortdesc}



Your VPC cluster is created with both a public and a private cloud service endpoint. Public service endpoints can't later be disabled, and therefore, you can't convert a public cluster to a private cluster. If you want to create a VPC cluster with no public cloud service endpoint and only a private cloud service endpoint, you must create the cluster [in the CLI](#cluster_vpcg2_cli) and include the `--disable-public-service-endpoint` flag.
{: important}



1. Make sure that you complete the prerequisites to [prepare your account](#cluster_prepare) and decide on your [cluster setup](#prepare_cluster_level).
1. [Create a Virtual Private Cloud (VPC) on generation 2 compute](https://cloud.ibm.com/vpc/provision/vpc){: external} with a subnet that is located in the VPC zone where you want to create the cluster.
    * During the VPC creation, three subnets are created by default. Subnets are specific to a zone. If you want to create a multizone cluster, create the subnet in one of the multizone-capable zones that you want to use. Later, you manually create the subnets for the remaining zones that you want to include in your cluster.
    
        Do not delete the subnets that you attach to your cluster during cluster creation or when you add worker nodes in a zone. If you delete a VPC subnet that your cluster used, any load balancers that use IP addresses from the subnet might experience issues, and you might be unable to create new load balancers.
        {: important}
        
    * If worker nodes must access public endpoints, or if you plan to enable both the public and private cloud service endpoints, you must attach a public gateway to each subnet to access default {{site.data.keyword.redhat_openshift_notm}} components such as the web console or OperatorHub.
    * If you require access to classic infrastructure resources, you must follow the steps in [Creating VPC subnets for classic access](/docs/openshift?topic=openshift-vpc-subnets#ca_subnet_ui) to create a classic access VPC and VPC subnets without the automatic default address prefixes.
    * For more information, see [Creating a VPC using the IBM Cloud console](/docs/vpc?topic=vpc-creating-a-vpc-using-the-ibm-cloud-console) and [Overview of VPC networking in {{site.data.keyword.openshiftlong_notm}}: Subnets](/docs/openshift?topic=openshift-vpc-subnets#vpc_basics_subnets).
1. If you want to create a multizone cluster, create the subnets for all the remaining zones that you want to include in your cluster. You must have one VPC subnet in all the zones where you want to create your multizone cluster.
    1. From the [VPC subnet dashboard](https://cloud.ibm.com/vpc/network/subnets){: external}, click **New subnet**.
    2. Enter a name for your subnet.
    3. Select the location of your VPC and zone where you want to create the subnet.
    4. Select the name of the VPC that you created.
    5. Specify the number of IP addresses to create. VPC subnets provide IP addresses for your worker nodes and load balancer services in the cluster, so [create a VPC subnet with enough IP addresses](/docs/openshift?topic=openshift-vpc-subnets#vpc_basics_subnets), such as 256. You can't change the number of IPs that a VPC subnet has later. If you enter a specific IP range, don't use the following reserved ranges: `172.16.0.0/16`, `172.18.0.0/16`, `172.19.0.0/16`, and `172.20.0.0/16`.
    6. Choose if you want to attach a public network gateway to your subnet. If you plan to enable both the public and private cloud service endpoints, you must attach a public gateway to each subnet to access default {{site.data.keyword.redhat_openshift_notm}} components such as the web console or OperatorHub. Additionally, a public network gateway is required when you want your cluster to access public endpoints, such as a public URL of another app or an {{site.data.keyword.cloud_notm}} service that supports public cloud service endpoints only. Make sure to review the [VPC networking basics](/docs/containers?topic=containers-plan_vpc_basics) to understand when a public network gateway is required and how you can set up your cluster to limit public access to one or more subnets only.
    7. Click **Create subnet**.
1. From the [{{site.data.keyword.redhat_openshift_notm}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, click **Create cluster**.
1. Configure your cluster environment.
    1. Select the **Standard** cluster plan.
    1. From the {{site.data.keyword.redhat_openshift_notm}} drop-down list, select the version that you want to use in your cluster.
    1. **Optional**: For the **OCP entitlement** section, you can select an entitlement for a worker pool, if you have one. Usually, leave the value set to **Purchase additional licenses for this worker pool**. If you have an {{site.data.keyword.cloud_notm}} Pak with an {{site.data.keyword.redhat_openshift_notm}} entitlement that you want to use, you can select **Apply my Cloud Pak OCP entitlement to this worker pool**. Later, when you configure the worker pool, make sure to select only the flavor and number of worker nodes that your entitlement permits.
    1. Select **VPC** infrastructure.
    1. From the **Virtual private cloud** drop-down menu, select the VPC that you created earlier.
1. Configure the **Location** details for your cluster.
    1. Select the **Resource group** that you want to create your cluster in.
        * A cluster can be created in only one resource group, and after the cluster is created, you can't change its resource group.
        * To create clusters in a resource group other than the default, you must have at least the [**Viewer** role](/docs/openshift?topic=openshift-users#checking-perms) for the resource group.
    2. Select the zones to create your cluster in.
        * The zones are filtered based on the VPC that you selected, and include the VPC subnets that you previously created.
        * To create a [single zone cluster](/docs/openshift?topic=openshift-ha_clusters#single_zone), select one zone only. If you select only one zone, you can [add zones to your cluster](/docs/openshift?topic=openshift-add_workers#add_zone) after the cluster is created.
        * To create a [multizone cluster](/docs/openshift?topic=openshift-ha_clusters#multizone), select multiple zones.
1. Configure your **Worker pool** setup. Worker pools are groups of worker nodes that share the same configuration. You can always add more worker pools to your cluster later.
    1. If you want a larger size for your worker nodes, click **Change flavor**. The flavor defines the amount of virtual CPU, memory, and disk space that is set up in each worker node and made available to the containers. Available bare metal and virtual machines types vary by the zone in which you deploy the cluster. For more information, see [Planning your worker node setup](/docs/containers?topic=containers-planning_worker_nodes). After you create your cluster, you can add different flavors by adding a worker pool to the cluster.
        * **Default**: The default flavor is **Virtual - shared, Ubuntu 18**, which comes with **4 vCPUs** of computing power and **16 GB** of memory. This virtual flavor is billed hourly. Other types of flavors include the following.
        * **Bare metal**: Bare metal servers are provisioned manually by IBM Cloud infrastructure after you order, and can take more than one business day to complete. Bare metal is best suited for high-performance applications that need more resources and host control. Be sure that you want to provision a bare metal machine. Because it is billed monthly, if you cancel it immediately after an order by mistake, you are still charged the full month.
        * **Virtual - shared**: Infrastructure resources, such as the hypervisor and physical hardware, are shared across you and other IBM customers, but each worker node is accessible only by you. Although this option is less expensive and sufficient in most cases, you might want to verify your performance and infrastructure requirements with your company policies. Virtual machines are billed hourly.
        * **Virtual - dedicated**: Your worker nodes are hosted on infrastructure that is devoted to your account. Your physical resources are completely isolated. Virtual machines are billed hourly.
    2. Set how many worker nodes to create per zone, such as **3**. For example, if you selected 2 zones and want to create 3 worker nodes, a total of 6 worker nodes are provisioned in your cluster with 3 worker nodes in each zone. You must set at least 2 worker nodes. For more information, see [What is the smallest size cluster that I can make?](/docs/openshift?topic=openshift-faqs#smallest_cluster).
    3. Select a key management service (KMS) instance and root key to encrypt the local disk for each worker node in the `default` worker pool.

    Before you can use KMS encryption, you must create a KMS instance and set up the required service authorization in IAM. See [Managing encryption for the worker nodes in your cluster](/docs/openshift?topic=openshift-encryption#worker-encryption).
    {: note}

1. If you don't have the required infrastructure permissions to create a cluster, the **Infrastructure permissions checker** lists the missing permissions. Ask your account owner to [set up the API key](/docs/containers?topic=containers-access-creds) with the required permissions.
1. Complete the **Resource details** to customize the unique cluster name and any [tags](/docs/account?topic=account-tag) that you want to use to organize your {{site.data.keyword.cloud_notm}} resources, such as the team or billing department.
1. In the **Summary** pane, review the order summary and then click **Create**. A worker pool is created with the number of workers that you specified. You can see the progress of the worker node deployment in the **Worker nodes** tab.
    - Your cluster might take some time to provision the {{site.data.keyword.redhat_openshift_notm}} master and all worker nodes and enter a   **Normal** state. Note that even if the cluster is ready, some parts of the cluster that are used by other services, such as Ingress  secrets or registry image pull secrets, might still be in process. Before you continue, wait until the cluster is ready by checking that the **Ingress subdomain** follows a pattern of `<cluster_name>.<region>.containers.appdomain.cloud`.
    - Every worker node is assigned a unique worker node ID and domain name that must not be changed manually after the cluster is created. Changing the ID or domain name prevents the {{site.data.keyword.redhat_openshift_notm}} master from managing your cluster.
        Is your cluster not in a **Normal** state? Check out the [Debugging clusters](/docs/containers?topic=containers-debug_clusters) guide for help. For example, if your cluster is provisioned in an account that is protected by a firewall gateway appliance, you must [configure your firewall settings to allow outgoing traffic to the appropriate ports and IP addresses](/docs/openshift?topic=openshift-firewall#firewall_outbound).
        {: tip}
        
1. After your cluster is created, you can [begin working with your cluster by configuring your CLI session](/docs/openshift?topic=openshift-access_cluster). For more possibilities, review the [Next steps](/docs/openshift?topic=openshift-clusters#next_steps).
1. {{site.data.keyword.redhat_openshift_notm}} version 4.4 or earlier only: To allow any traffic requests to apps that you deploy on your worker nodes, modify the VPC's default security group.
    1. From the [Virtual private cloud dashboard](https://cloud.ibm.com/vpc-ext/network/vpcs){: external}, click the name of the **Default Security Group** for the VPC that you created.
    2. In the **Inbound rules** section, click **New rule**.
    3. Choose the **TCP** protocol, enter `30000` for the **Port min** and `32767` for the **Port max**, and leave the **Any** source type selected.
    4. Click **Save**.
    5. If you require VPC VPN access or classic infrastructure access into this cluster, repeat these steps to add a rule that uses the **UDP** protocol, `30000` for the **Port min**, `32767` for the **Port max**, and the **Any** source type.

### Creating standard VPC clusters from the CLI
{: #cluster_vpcg2_cli}

![VPC infrastructure provider icon.](images/icon-vpc-2.svg) Create your single zone or multizone VPC cluster by using the {{site.data.keyword.cloud_notm}} CLI.
{: shortdesc}

**Before you begin**:
* Make sure that you complete the prerequisites to [prepare your account](#cluster_prepare) and decide on your [cluster setup](#prepare_cluster_level).
* Install the {{site.data.keyword.cloud_notm}} CLI and the [{{site.data.keyword.openshiftlong_notm}} plug-in](/docs/containers?topic=containers-cs_cli_install#cs_cli_install).
* Install the [VPC CLI plug-in](/docs/vpc?topic=vpc-infrastructure-cli-plugin-vpc-reference#cli-ref-prereqs).


**To create a VPC cluster from the CLI**:

1. In your command line, log in to your {{site.data.keyword.cloud_notm}} account and target the {{site.data.keyword.cloud_notm}} region and resource group where you want to create your VPC cluster. For supported regions, see [Creating a VPC in a different region](/docs/vpc?topic=vpc-creating-a-vpc-in-a-different-region). Enter your {{site.data.keyword.cloud_notm}} credentials when prompted. If you have a federated ID, use the --sso flag to log in.
    ```sh
    ibmcloud login -r <region> [-g <resource_group>] [--sso]
    ```
    {: pre}

2. [Create a VPC](/docs/vpc?topic=vpc-creating-vpc-resources-with-cli-and-api&interface=cli#create-a-vpc-cli) in the same region where you want to create the cluster.
    Do the clusters of worker nodes in your VPC need to send and receive information to and from IBM Cloud classic infrastructure? Follow the steps in [Creating VPC subnets for classic access](/docs/openshift?topic=openshift-vpc-subnets#ca_subnet_cli) to create a classic-enabled VPC and VPC subnets without the automatic default address prefixes.
    {: important}
    
3. [Create a subnet for your VPC](/docs/vpc?topic=vpc-creating-vpc-resources-with-cli-and-api&interface=cli#create-a-subnet-cli).
    * If you want to create a [multizone cluster](/docs/openshift?topic=openshift-ha_clusters#multizone), repeat this step to create additional subnets in all the zones that you want to include in your cluster.
    * VPC subnets provide IP addresses for your worker nodes and load balancer services in the cluster, so [create a VPC subnet with enough IP addresses](/docs/openshift?topic=openshift-vpc-subnets#vpc_basics_subnets), such as 256. You can't change the number of IPs that a VPC subnet has later.
    * Do not use the following reserved ranges: `172.16.0.0/16`, `172.18.0.0/16`, `172.19.0.0/16`, and `172.20.0.0/16`.
    * If worker nodes must access public endpoints, or if you plan to enable both the public and private cloud service endpoints, you must [attach a public gateway](/docs/vpc?topic=vpc-creating-vpc-resources-with-cli-and-api&interface=cli#attach-public-gateway-cli) to each subnet to access default {{site.data.keyword.redhat_openshift_notm}} components such as the web console or OperatorHub.
    * **Important**: Do not delete the subnets that you attach to your cluster during cluster creation or when you add worker nodes in a zone. If you delete a VPC subnet that your cluster used, any load balancers that use IP addresses from the subnet might experience issues, and you might be unable to create new load balancers.
    * For more information, see [Overview of VPC networking in {{site.data.keyword.openshiftlong_notm}}: Subnets](/docs/openshift?topic=openshift-vpc-subnets#vpc_basics_subnets).
4. Create the cluster in your VPC. You can use the `ibmcloud oc cluster create vpc-gen2` command to create a single zone cluster in your VPC with worker nodes that are connected to one VPC subnet only. If you want to create a multizone cluster, you can use the {{site.data.keyword.cloud_notm}} console, or [add more zones](/docs/openshift?topic=openshift-add_workers#vpc_add_zone) to your cluster after the cluster is created. The cluster takes a few minutes to provision.
    ```sh
    ibmcloud oc cluster create vpc-gen2 --name <cluster_name> --zone <vpc_zone> --vpc-id <vpc_ID> --subnet-id <vpc_subnet_ID> --flavor <worker_flavor> --version 4.8_openshift --cos-instance <COS_CRN> --workers <number_workers_per_zone> [--pod-subnet] [--service-subnet] [--disable-public-service-endpoint] [--kms-instance <KMS_instance_ID> --crk <root_key_ID>]
    ```
    {: pre}

    `--name <cluster_name>`
    :   Specify a name for your cluster. The name must start with a letter, can contain letters, numbers, periods (.), and hyphen (-), and must be 35 characters or fewer. Use a name that is unique across regions. The cluster name and the region in which the cluster is deployed form the fully qualified domain name for the Ingress subdomain. To ensure that the Ingress subdomain is unique within a region, the cluster name might be truncated and appended with a random value within the Ingress domain name.

    `--zone <zone>`
    :   Specify the {{site.data.keyword.cloud_notm}} zone where you want to create your cluster. Make sure that you use a zone that matches the metro city location that you selected when you created your VPC and that you have an existing VPC subnet for that zone. For example, if you created your VPC in the Dallas metro city, your zone must be set to `us-south-1`, `us-south-2`, or `us-south-3`. To list available VPC cluster zones, run `ibmcloud oc zone ls --provider vpc-gen2`. Note that when you select a zone outside of your country, you might require legal authorization before data can be physically stored in a foreign country.

    `--vpc-id <vpc_ID>`
    :   Enter the ID of the VPC that you created earlier. To retrieve the ID of your VPC, run `ibmcloud oc vpcs`. 

    `--subnet-id <subnet_ID>`
    :   Enter the ID of the VPC subnet that you created earlier. When you create a VPC cluster from the CLI, you can initially create your cluster in one zone with one subnet only. To create a multizone cluster, [add more zones with the subnets](/docs/containers?topic=containers-add_workers) that you created earlier to your cluster after the cluster is created. To list the IDs of your subnets in all resource groups, run ` ibmcloud oc subnets --provider vpc-gen2 --vpc-id &lt,VPC_ID> --zone <subnet_zone> `.  

    `--flavor <worker_flavor>`
    :   Enter the worker node flavor that you want to use. The flavor determines the amount of virtual CPU, memory, and disk space that is set up in each worker node and made available to your apps. VPC worker nodes can be created as virtual machines on shared infrastructure only. Bare metal or software-defined storage machines are not supported.  For more information, see [Planning your worker node setup](/docs/containers?topic=containers-planning_worker_nodes). To view available flavors, first list available VPC zones with `ibmcloud oc zone ls --provider vpc-gen2`, and then use the zone to list supported flavors by running `ibmcloud oc flavors --zone <VPC_zone> --provider vpc-gen2`. After you create your cluster, you can add different flavors by adding a worker node or worker pool to the cluster.

    `--version 4.8_openshift`
    :   VPC clusters are supported for {{site.data.keyword.redhat_openshift_notm}} version 4 only.
    
    
    `--cos-instance <cos_CRN>`
    :   Include the CRN ID of a standard {{site.data.keyword.cos_full_notm}} instance to back up the internal registry of your cluster. To list the CRN of existing instances, run `ibmcloud resource service-instances --long` and find the **ID** of your object storage instance. To create a standard object storage instance, run `ibmcloud resource service-instance-create <name> cloud-object-storage standard global` and note its **ID**.
    
    
    `--workers <number>`
    :   Specify at least 2 worker nodes to include in the cluster. For more information, see [What is the smallest size cluster that I can make?](/docs/openshift?topic=openshift-faqs#smallest_cluster). This value is optional.

    `--pod-subnet`
    :   In the first cluster that you create in a VPC, the default pod subnet is `172.17.0.0/18`. In the second cluster that you create in that VPC, the default pod subnet is `172.17.64.0/18`. In each subsequent cluster, the pod subnet range is the next available, non-overlapping `/18` subnet. If you plan to connect your cluster to on-premises networks through {{site.data.keyword.BluDirectLink}} or a VPN service, you can avoid subnet conflicts by specifying a custom subnet CIDR that provides the private IP addresses for your pods.
    When you choose a subnet size, consider the size of the cluster that you plan to create and the number of worker nodes that you might add in the future. The subnet must have a CIDR of at least `/23`, which provides enough pod IPs for a maximum of four worker nodes in a cluster. For larger clusters, use `/22` to have enough pod IP addresses for eight worker nodes, `/21` to have enough pod IP addresses for 16 worker nodes, and so on. Note that the pod and service subnets can't overlap. If you use custom-range subnets for your worker nodes, [you must ensure that your worker node subnets don't overlap with your cluster's pod subnet](/docs/openshift?topic=openshift-vpc-subnets#vpc-ip-range). The subnet that you choose must be within one of the following ranges:
        - `172.17.0.0 - 172.17.255.255`
        - `172.21.0.0 - 172.31.255.255`
        - `192.168.0.0 - 192.168.254.255`
        - `198.18.0.0 - 198.19.255.255`

    `--service-subnet`
    :   All services that are deployed to the cluster are assigned a private IP address in the 172.21.0.0/16 range by default. If you plan to connect your cluster to on-premises networks through {{site.data.keyword.dl_full_notm}} or a VPN service, you can avoid subnet conflicts by specifying a custom subnet CIDR that provides the private IP addresses for your services.
    The subnet must be specified in CIDR format with a size of at least `/24`, which allows a maximum of 255 services in the cluster, or larger. The subnet that you choose must be within one of the following ranges:
    - `172.17.0.0 - 172.17.255.255`
    - `172.21.0.0 - 172.31.255.255`
    - `192.168.0.0 - 192.168.254.255`
    - `198.18.0.0 - 198.19.255.255`Note that the pod and service subnets can't overlap.

    `--disable-public-service-endpoint`
    :   Include this option in your command to create your VPC cluster with a private cloud service endpoint only. If you don't include this option, your cluster is set up with a public and a private cloud service endpoint. The service endpoint determines how your {{site.data.keyword.redhat_openshift_notm}} master and the worker nodes communicate, how your cluster access other {{site.data.keyword.cloud_notm}} services and apps outside the cluster, and how your users connect to your cluster. For more information, see [Planning your cluster network setup](/docs/containers?topic=containers-plan_clusters).
        If you include this flag, your cluster is created with routers and Ingress controllers that expose your apps on the private network only by default. If you later want to expose apps to a public network, you must manually create public routers and Ingress controllers.
        {: important}
        

    `--kms-instance <KMS_instance_ID>`
    :   Optional: Include the ID of a key management service (KMS) instance to use to encrypt the local disk on the worker nodes in the `default` worker pool. To list available KMS instances, run `ibmcloud oc kms instance ls`. If you include this option, you must also include the `--crk` option.
        Before you can use KMS encryption, you must create a KMS instance and set up the required service authorization in IAM. See [Managing encryption](/docs/openshift?topic=openshift-encryption#worker-encryption) for the worker nodes in your cluster.
        {: note}
  

    `--crk <root_key>`
    :   Optional: Include the ID of the root key in the KMS instance to use to encrypt the local disk on the worker nodes in the `default` worker pool. To list available root keys, run `ibmcloud oc kms crk ls --instance-id`. If you include this option, you must also include the `--kms-instance` option.
        Before you can use KMS encryption, you must create a KMS instance and set up the required service authorization in IAM. See [Managing encryption](/docs/openshift?topic=openshift-encryption#worker-encryption) for the worker nodes in your cluster.
        {: note}
    
5. Verify that the creation of the cluster was requested. It can take a few minutes for the worker node machines to be ordered, and for the cluster to be set up and provisioned in your account.
    ```sh
    ibmcloud oc cluster ls
    ```
    {: pre}

    When the provisioning of your {{site.data.keyword.redhat_openshift_notm}} master is completed, the state of your cluster changes to **normal**. After the {{site.data.keyword.redhat_openshift_notm}} master is ready, your worker nodes are set up.
    ```sh
    NAME         ID                                   State      Created          Workers    Zone      Version     Resource Group Name   Provider
    mycluster    aaf97a8843a29941b49a598f516da72101   normal   20170201162433   3          Dallas     4.7.36_xxxx_openshift      Default               vpc-gen2
    ```
    {: screen}

    Is your cluster not in a **normal** state? Check out the [Debugging clusters](/docs/containers?topic=containers-debug_clusters) guide for help. For example, if your cluster is provisioned in an account that is protected by a firewall gateway appliance, you must [configure your firewall settings to allow outgoing traffic to the appropriate ports and IP addresses](/docs/openshift?topic=openshift-firewall#firewall_outbound).
    {: tip}

6. Check the status of the worker nodes.
    ```sh
    ibmcloud oc worker ls --cluster <cluster_name_or_ID>
    ```
    {: pre}

    When the worker nodes are ready, the worker node **State** changes to `normal` and the **Status** changes to `Ready`. When the node **Status** changes to `Ready`, you can access the cluster. Note that even if the cluster is ready, some parts of the cluster that are used by other services, such as Ingress secrets or registry image pull secrets, might still be in process.
    ```sh
    ID                                                     Public IP        Private IP     Flavor              State    Status   Zone    Version
    kube-blrs3b1d0p0p2f7haq0g-mycluster-default-000001f7   169.xx.xxx.xxx  10.xxx.xx.xxx   b3c.4x16.encrypted  normal   Ready    dal10   4.7.36_xxxx_openshift
    ```
    {: screen}

    Every worker node is assigned a unique worker node ID and domain name that must not be changed manually after the cluster is created. Changing the ID or domain name prevents the {{site.data.keyword.redhat_openshift_notm}} master from managing your cluster.
    {: important}

7. **Optional**: If you created your cluster in a [multizone metro location](/docs/openshift?topic=openshift-regions-and-zones#zones-vpc), you can [spread the default worker pool across zones](/docs/openshift?topic=openshift-add_workers#vpc_add_zone) to increase the cluster's availability.

8. After your cluster is created, you can [begin working with your cluster by configuring your CLI session](/docs/openshift?topic=openshift-access_cluster).

9. {{site.data.keyword.redhat_openshift_notm}} version 4.4 or earlier only: To allow any traffic requests to apps that you deploy on your worker nodes, modify the VPC's default security group.
    1. List your security groups. For the **VPC** that you created, note the ID of the default security group.
        ```sh
        ibmcloud is security-groups
        ```
        {: pre}

        Example output with only the default security group of a randomly generated name, `preppy-swimmer-island-green-refreshment`:
        ```sh
        ID                                     Name                                       Rules   Network interfaces         Created                     VPC                      Resource group
        1a111a1a-a111-11a1-a111-111111111111   preppy-swimmer-island-green-refreshment    4       -                          2019-08-12T13:24:45-04:00   <vpc_name>(bbbb222b-.)   c3c33cccc33c333ccc3c33cc3c333cc3
        ```
        {: screen}

    2. Add a security group rule to allow inbound TCP traffic on ports 30000-32767.
        ```sh
        ibmcloud is security-group-rule-add <security_group_ID> inbound tcp --port-min 30000 --port-max 32767
        ```
        {: pre}

    3. If you require VPC VPN access or classic infrastructure access into this cluster, add a security group rule to allow inbound UDP traffic on ports 30000-32767.
        ```sh
        ibmcloud is security-group-rule-add <security_group_ID> inbound udp --port-min 30000 --port-max 32767
        ```
        {: pre}

Your cluster is ready for your workloads! You might also want to [add a tag to your cluster](/docs/openshift?topic=openshift-add_workers#cluster_tags), such as the team or billing department that uses the cluster, to help manage {{site.data.keyword.cloud_notm}} resources. For more ideas of what to do with your cluster, review the [Next steps](/docs/openshift?topic=openshift-clusters#next_steps). 



## Next steps
{: #next_steps}

When the cluster is up and running, you can check out the following cluster administration tasks:
- If you created the cluster in a multizone capable zone, [spread worker nodes by adding a zone to your cluster](/docs/containers?topic=containers-add_workers).
- [Deploy an app in your cluster.](/docs/containers?topic=containers-deploy_app#app_cli)
- [Set up your own private registry in {{site.data.keyword.cloud_notm}} to store and share Docker images with other users.](/docs/Registry?topic=Registry-getting-started)
- [Set up the cluster autoscaler](/docs/containers?topic=containers-cluster-scaling-classic-vpc) to automatically add or remove worker nodes from your worker pools based on your workload resource requests.
- Control who can create pods in your cluster with [pod security policies](/docs/containers?topic=containers-psp).

Then, you can check out the following network configuration steps for your cluster setup:
* ![Classic infrastructure provider icon.](images/icon-classic-2.svg) Classic clusters:
    * Isolate networking workloads to edge worker nodes [in classic clusters without a gateway](/docs/containers?topic=containers-edge).
    * Expose your apps with [public networking services](/docs/openshift?topic=openshift-cs_network_planning#openshift_routers) or [private networking services](/docs/openshift?topic=openshift-cs_network_planning#private_access).
    * Connect your cluster with services in private networks outside of your {{site.data.keyword.cloud_notm}} account by setting up [{{site.data.keyword.dl_full_notm}}](/docs/dl?topic=dl-get-started-with-ibm-cloud-dl) or the [strongSwan IPSec VPN service](/docs/containers?topic=containers-vpn).
    * Create Calico host network policies to isolate your cluster on the [public network](/docs/openshift?topic=openshift-network_policies#isolate_workers_public) and on the [private network](/docs/openshift?topic=openshift-network_policies#isolate_workers).
* ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC clusters:
    * [Back up your internal image registry to {{site.data.keyword.cos_full_notm}}.](/docs/openshift?topic=openshift-registry#cos_image_registry)
    * Expose your apps with [public networking services](/docs/openshift?topic=openshift-cs_network_planning#openshift_routers) or [private networking services](/docs/openshift?topic=openshift-cs_network_planning#private_access).
    * Connect your cluster with services in private networks outside of your {{site.data.keyword.cloud_notm}} account or with resources in other VPCs by [setting up the {{site.data.keyword.vpc_short}} VPN](/docs/containers?topic=containers-vpc-vpnaas).
    * [Add rules to the security group for your worker nodes](/docs/containers?topic=containers-vpc-network-policy) to control ingress and egress traffic to your VPC subnets.




