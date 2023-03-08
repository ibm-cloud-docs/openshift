---

copyright: 
  years: 2014, 2023
lastupdated: "2023-03-08"

keywords: openshift, clusters, classic, create

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}



# Creating classic clusters
{: #cluster-create-classic}

[Classic infrastructure]{: tag-classic-inf}


Use the {{site.data.keyword.cloud_notm}} CLI or the {{site.data.keyword.cloud_notm}} console to create a fully customizable standard cluster with your choice of hardware isolation and access to features like multiple worker nodes for a highly available environment.
{: shortdesc}



## Creating a classic cluster in the console
{: #clusters_ui}
{: ui}

Create your single zone or multizone classic {{site.data.keyword.redhat_openshift_notm}} cluster by using the {{site.data.keyword.cloud_notm}} console.
{: shortdesc}

{{site.data.keyword.openshiftlong_notm}} clusters are created with a public only or both a public and private service endpoint. Public service endpoints can't be disabled, and therefore, you can't convert a public {{site.data.keyword.redhat_openshift_notm}} cluster to a private one. If you want your cluster to remain private, see [Planning your cluster network setup](/docs/containers?topic=containers-plan_vpc_basics#vpc-pgw).
{: important}

1. Complete the prerequisites to [prepare your account](/docs/containers?topic=containers-clusters&interface=ui) and decide on your cluster setup.
2. From the [{{site.data.keyword.redhat_openshift_notm}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, click **Create cluster**.
3. Configure your cluster environment.
    1. From the {{site.data.keyword.redhat_openshift_notm}} drop-down list, select the version that you want to use in your cluster, such as 4.10.52.
    1. **Optional**: For the **OCP entitlement** section, you can select an entitlement for a worker pool, if you have one. Usually, leave the value set to **Purchase additional licenses for this worker pool**. If you have an {{site.data.keyword.cloud_notm}} Pak with a {{site.data.keyword.redhat_openshift_notm}} entitlement that you want to use, you can select **Apply my Cloud Pak OCP entitlement to this worker pool**. Later, when you configure the worker pool, make sure to select only the flavor and number of worker nodes that your entitlement permits.
4. Configure the **Location** details for your cluster.
    1. Select the **Resource group** that you want to create your cluster in.
        * A cluster can be created in only one resource group, and after the cluster is created, you can't change its resource group.
        * To create clusters in a resource group other than the default, you must have at least the [**Viewer** role](/docs/openshift?topic=openshift-users#checking-perms) for the resource group.
    2. Select a **Geography** to create the cluster in, such as **North America**. The geography helps filter the **Availability** and **Metro** values that you can select.
    3. Select the **Availability** that you want for your cluster, **Single zone** or **Multizone**. In a multizone cluster, the {{site.data.keyword.redhat_openshift_notm}} master is deployed in a multizone-capable zone and three replicas of your master are spread across zones.
    4. Enter the **Metro** and **Worker zones** details, depending on the availability that you selected for your cluster.
        - **Multizone clusters**:
            1. Select a **Metro** location. For the best performance, select the metro location that is physically closest to you. Your choices might be limited by geography.
            2. Select the specific **Worker zones** within the metro to host your cluster. You must select at least one zone, but you can select as many as you like. If you select more than one zone, the worker nodes are spread across the zones that you choose, which gives you higher availability. If you select only one zone, you can [add zones to your cluster](/docs/openshift?topic=openshift-add_workers#add_zone) after the cluster is created.
        - **Single zone clusters**: Select a **Worker zone** in which you want to host your cluster. For the best performance, select the data center that is physically closest to you. Your choices might be limited by geography.
    5. For each of the selected zones, choose your public and private VLANs. You can change the pre-selected VLANs by clicking the **Edit VLANs** pencil icon. The first time that you create a cluster in a zone, public and private VLANs are automatically created for you. Worker nodes communicate with each other by using the private VLAN, and can communicate with the {{site.data.keyword.redhat_openshift_notm}} master by using the public or the private VLAN. If you don't have a public or private VLAN in this zone, a public and a private VLAN are automatically created for you. You can use the same VLAN for multiple clusters.
5. Configure your **Worker pool** setup. Worker pools are groups of worker nodes that share the same configuration. You can always add more worker pools to your cluster later.
    1. If you want a larger size for your worker nodes or if you want to change worker node operating systems, click **Change flavor**. The flavor defines the amount of virtual CPU, memory, and disk space that is set up in each worker node and made available to the containers. Available bare metal and virtual machines types vary by the zone in which you deploy the cluster. For more information, see [Planning your worker node setup](/docs/openshift?topic=openshift-planning_worker_nodes). After you create your cluster, you can add different flavors by adding a worker pool to the cluster.
            * **Default**: The default flavor comes with **4 vCPUs** of computing power and **16 GB** of memory. This virtual flavor is billed hourly. Other types of flavors include the following options.
            * **Bare metal**: Bare metal servers are provisioned manually by IBM Cloud infrastructure after you order, and can take more than one business day to complete. Bare metal is best suited for high-performance applications that need more resources and host control. Be sure that you want to provision a bare metal machine. Because it is billed monthly, if you cancel it immediately after an order by mistake, you are still charged the full month.
            * **Virtual - shared**: Infrastructure resources, such as the hypervisor and physical hardware, are shared across you and other IBM customers, but each worker node is accessible only by you. Although this option is usually less expensive and sufficient, you might want to verify your performance and infrastructure requirements with your company policies. Virtual machines are billed hourly.
            * **Virtual - dedicated**: Your worker nodes are hosted on infrastructure that is devoted to your account. Your physical resources are completely isolated. Virtual machines are billed hourly.
    2. Set how many worker nodes to create per zone, such as **3**. For example, if you selected 2 zones and want to create 3 worker nodes, a total of 6 worker nodes are provisioned in your cluster with 3 worker nodes in each zone. You must set at least 2 worker nodes. For more information, see [What is the smallest size cluster that I can make?](/docs/openshift?topic=openshift-faqs#smallest_cluster).
    3. Toggle disk encryption. By default, [worker nodes feature AES 256-bit disk encryption](/docs/openshift?topic=openshift-security#workernodes).

    
6. Configure your cluster with a public only or both a public and a private cloud service endpoint by setting the **Master service endpoint**. For more information about what setup is required to run internet-facing apps, or to keep your cluster private, see [Planning your cluster network setup](/docs/containers?topic=containers-plan_vpc_basics#vpc-pgw). After you create the cluster, you can't later change the cloud service endpoints.

7. If you don't have the required infrastructure permissions to create a cluster, the **Infrastructure permissions checker** lists the missing permissions. Ask your account owner to [set up the API key](/docs/openshift?topic=openshift-access-creds) with the required permissions.

8. Complete the **Resource details** to customize the unique cluster name and any [tags](/docs/account?topic=account-tag) that you want to use to organize your {{site.data.keyword.cloud_notm}} resources, such as the team or billing department.

9. Enable any integrations that you want to include on your cluster.
    - [Activity tracking]{: tag-green} Enable the [activity tracking](/docs/activity-tracker?topic=activity-tracker-getting-started) option. From the drop down menu under **Instance**, choose an existing instance or **Create a new instance**. If you choose **Create a new instance**, the details of the new instance are shown. The new instance is created when the cluster is created. 
    - [Logging]{: tag-dark-teal} Enable the [logging](/docs/log-analysis?topic=log-analysis-getting-started) option. From the drop down **Platform instance** menu, choose a platform instance. From the drop down **Application instance**, choose an existing application instance or choose **Create a new instance**. If you choose **Create a new instance**, the details of the new instance are shown. The new instance is created when the cluster is created. 
    - [Monitoring]{: tag-magenta} Enable the [monitoring](/docs/monitoring?topic=monitoring-getting-started) option. From the drop down **Platform instance** menu, choose a platform instance. From the drop down **Application instance**, choose an existing application instance or choose **Create a new instance**. If you choose **Create a new instance**, the details of the new instance are shown. The new instance is created when the cluster is created.
    - [Secrets Manager]{: tag-teal} Enable [Secrets Manager](/docs/containers?topic=containers-certs-mgr-migration). From the **Secrets Manager instance** drop down menu, choose an existing instance that you want to register to the cluster. If no instances are available, [create one](/docs/containers?topic=containers-secrets-mgr). If you want to apply a secret group, choose one from the **Secrets Manager group** drop down menu.

10. In the **Summary** pane, review your order summary and then click **Create**. A worker pool is created with the number of workers that you specified. You can see the progress of the worker node deployment in the **Worker nodes** tab.
    - Your cluster might take some time to provision the {{site.data.keyword.redhat_openshift_notm}} master and all worker nodes and enter a **Normal** state. Note that even if the cluster is ready, some parts of the cluster that are used by other services, such as Ingress  secrets or registry image pull secrets, might still be in process. Before you continue, wait until the cluster is ready by checking that the **Ingress subdomain** follows a pattern of `<cluster_name>.<region>.containers.appdomain.cloud`.
    - Every worker node is assigned a unique worker node ID and domain name that must not be changed manually after the cluster is created. Changing the ID or domain name prevents the {{site.data.keyword.redhat_openshift_notm}} master from managing your cluster.
        Is your cluster not in a **Normal** state? Check out the [Debugging clusters](/docs/openshift?topic=openshift-debug_clusters) guide for help. For example, if your cluster is provisioned in an account that is protected by a firewall gateway appliance, you must [configure your firewall settings to allow outgoing traffic to the appropriate ports and IP addresses](/docs/openshift?topic=openshift-firewall#firewall_outbound).
        {: tip}
        
11. After your cluster is created, you can [begin working with your cluster by configuring your CLI session](/docs/openshift?topic=openshift-access_cluster). For more possibilities, review the [Next steps](/docs/openshift?topic=openshift-clusters#next_steps).



## Creating a standard classic cluster in the CLI
{: #clusters_cli_steps}
{: cli}

Create your single zone or multizone classic cluster by using the {{site.data.keyword.cloud_notm}} CLI.
{: shortdesc}

* Ensure that you complete the prerequisites to [prepare your account](/docs/containers?topic=containers-clusters&interface=ui) and decide on your cluster setup. Keep in mind that you need a cluster with a minimum of 2 worker nodes of the `4x16` flavor so that default {{site.data.keyword.redhat_openshift_notm}} components can deploy.
* Install the {{site.data.keyword.cloud_notm}} CLI and the [{{site.data.keyword.openshiftlong_notm}} plug-in](/docs/openshift?topic=openshift-openshift-cli).

1. Log in to the {{site.data.keyword.cloud_notm}} CLI. Enter your {{site.data.keyword.cloud_notm}} credentials when prompted. If you are logging in with a federated ID, use `ibmcloud login --sso`.

    ```sh
    ibmcloud login [--sso]
    ```
    {: pre}

1. If you have multiple {{site.data.keyword.cloud_notm}} accounts, select the account where you want to create your cluster.

1. To create clusters in a resource group other than default, target that resource group. A cluster can be created in only one resource group, and after the cluster is created, you can't change its resource group. You must have at least the [**Viewer** role](/docs/openshift?topic=openshift-users#checking-perms) for the resource group to target it.

    ```sh
    ibmcloud target -g <resource_group_name>
    ```
    {: pre} 

1. Review the zones where you can create your cluster. In the output of the following command, zones have a **Location Type** of `dc`. To span your cluster across zones, you must create the cluster in a [multizone-capable zone](/docs/openshift?topic=openshift-regions-and-zones#zones-mz). Multizone-capable zones have a metro value in the **Multizone Metro** column. If you want to create a multizone cluster, you can use the {{site.data.keyword.cloud_notm}} console, or [add more zones](/docs/openshift?topic=openshift-add_workers#add_zone) to your cluster after the cluster is created.
    ```sh
    ibmcloud oc locations
    ```
    {: pre}

    When you select a zone that is located outside your country, keep in mind that you might require legal authorization before data can be physically stored in a foreign country.
    {: note}

1. Review the worker node flavors that are available in that zone. The flavor determines the amount of virtual CPU, memory, and disk space that is set up in each worker node and made available to your apps. Worker nodes in classic clusters can be created as virtual machines on shared or dedicated infrastructure, or as bare metal machines that are dedicated to you. For more information, see [Planning your worker node setup](/docs/openshift?topic=openshift-planning_worker_nodes). After you create your cluster, you can add different flavors by [adding a worker pool](/docs/openshift?topic=openshift-add_workers#add_pool).

    Before you create a bare metal machine, be sure that you want to provision one. Bare metal machines are billed monthly. If you order a bare metal machine by mistake, you are charged for the entire month, even if you cancel the machine immediately.  
    {: tip}

    ```sh
    ibmcloud oc flavors --zone <zone>
    ```
    {: pre}

1. Check if you have existing VLANs in the zones that you want to include in your cluster, and note the ID of the VLAN. If you don't have a public or private VLAN in one of the zones that you want to use in your cluster, {{site.data.keyword.containerlong_notm}} automatically creates these VLANs for you when you create the cluster.
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

1. Create your standard cluster.
    ```sh
    ibmcloud oc cluster create classic --zone <zone> --flavor <flavor> --hardware <shared_or_dedicated> --public-vlan <public_VLAN_ID> --private-vlan <private_VLAN_ID> --workers <number> [--operating-system (REDHAT_7_64|REDHAT_8_64)] --name <cluster_name> --version <major.minor.patch>_openshift --public-service-endpoint [--private-service-endpoint] [--pod-subnet] [--service-subnet] [--disable-disk-encrypt] [--sm-group GROUP] [--sm-instance INSTANCE]
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
    :   In [VRF-enabled](/docs/account?topic=account-vrf-service-endpoint#vrf) and [service endpoint-enabled accounts](/docs/account?topic=account-vrf-service-endpoint#service-endpoint): Enable the private cloud service endpoint so that your {{site.data.keyword.redhat_openshift_notm}} master and the worker nodes can communicate over the private VLAN. If you specify this option, you must also enable the public cloud service endpoint by using the `--public-service-endpoint` option. Note that you can't later change the cloud service endpoints.After you create the cluster, you can get the endpoint by running `ibmcloud oc cluster get --cluster <cluster_name_or_ID>`.

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
    :   Include this option only if you use this cluster with an [IBM Cloud Pak](/docs/openshift?topic=openshift-openshift_cloud_paks) that has a {{site.data.keyword.redhat_openshift_notm}} entitlement. When you specify the number of workers (`--workers`) and flavor (`--flavor`), make sure to specify only the number and size of worker nodes that you are entitled to use in [IBM Passport Advantage](https://www.ibm.com/software/passportadvantage/index.html){: external}. After your cluster is created, you are not charged the {{site.data.keyword.redhat_openshift_notm}} license fee for the entitled worker nodes in the `default` worker pool.
    Do not exceed your entitlement. Keep in mind that your OpenShift Container Platform entitlements can be used with other cloud providers or in other environments. To avoid billing issues later, make sure that you use only what you are entitled to use. For example, you might have an entitlement for the OCP licenses for two worker nodes of 4 CPU and 16 GB memory, and you create this worker pool with two worker nodes of 4 CPU and 16 GB memory. You used your entire entitlement, and you can't use the same entitlement for other worker pools, cloud providers, or environments.
    {: important}

    `--sm-group GROUP`
    :    The secret group ID of the {{site.data.keyword.secrets-manager_short}} instance where your secrets are persisted. To get a secret group ID, see the [{{site.data.keyword.secrets-manager_short}} CLI reference](/docs/secrets-manager-cli-plugin?topic=secrets-manager-cli-plugin-secrets-manager-cli#secrets-manager-cli-secret-groups-command).

    `--sm-instance INSTANCE`
    :    The CRN of the {{site.data.keyword.secrets-manager_short}} instance. To get the CRN of an instance, run `ibmcloud oc ingress instance ls --cluster CLUSTER`.

1. Verify that the creation of the cluster was requested. For virtual machines, it can take a few minutes for the worker node machines to be ordered, and for the cluster to be set up and provisioned in your account. Bare metal physical machines are provisioned by manual interaction with IBM Cloud infrastructure, and can take more than one business day to complete.
    ```sh
    ibmcloud oc cluster ls
    ```
    {: pre}

    When the provisioning of your {{site.data.keyword.redhat_openshift_notm}} master is completed, the **State** of your cluster changes to `normal`. After your {{site.data.keyword.redhat_openshift_notm}} master is ready, the provisioning of your worker nodes is initiated.
    ```sh
    NAME         ID                         State      Created          Workers    Zone      Version     Resource Group Name   Provider
    mycluster    blrs3b1d0p0p2f7haq0g       normal   20170201162433   3          dal10     4.10.52_1544_openshift      Default             classic
    ```
    {: screen}

    Is your cluster not in a `normal` state? Check out the [Debugging clusters](/docs/openshift?topic=openshift-debug_clusters) guide for help. For example, if your cluster is provisioned in an account that is protected by a firewall gateway appliance, you must [configure your firewall settings to allow outgoing traffic to the appropriate ports and IP addresses](/docs/openshift?topic=openshift-firewall#firewall_outbound).
    {: tip}

1. Check the status of the worker nodes.
    ```sh
    ibmcloud oc worker ls --cluster <cluster_name_or_ID>
    ```
    {: pre}

    When the worker nodes are ready, the worker node state changes to **normal** and the status changes to **Ready**. When the node status is **Ready**, you can then access the cluster. Note that even if the cluster is ready, some parts of the cluster that are used by other services, such as Ingress secrets or registry image pull secrets, might still be in process. Note that if you created your cluster with a private VLAN only, no **Public IP** addresses are assigned to your worker nodes.
    ```sh
    ID                                                     Public IP        Private IP     Flavor              State    Status   Zone    Version
    kube-blrs3b1d0p0p2f7haq0g-mycluster-default-000001f7   169.xx.xxx.xxx  10.xxx.xx.xxx   u3c.2x4.encrypted   normal   Ready    dal10   1.25.6_1526
    ```
    {: screen}

    Every worker node is assigned a unique worker node ID and domain name that must not be changed manually after the cluster is created. If you change the ID or domain name, the {{site.data.keyword.redhat_openshift_notm}} master cannot manage your cluster.
    {: important}

1. **Optional**: If you created your cluster in a [multizone metro location](/docs/openshift?topic=openshift-regions-and-zones#zones-mz), you can [spread the default worker pool across zones](/docs/openshift?topic=openshift-add_workers#add_zone) to increase the cluster's availability.

1. After your cluster is created, you can [begin working with your cluster by configuring your CLI session](/docs/openshift?topic=openshift-access_cluster).

Your cluster is ready for your workloads! You might also want to [add a tag to your cluster](/docs/openshift?topic=openshift-add_workers#cluster_tags), such as the team or billing department that uses the cluster, to help manage {{site.data.keyword.cloud_notm}} resources. For more ideas of what to do with your cluster, review the [Next steps](/docs/openshift?topic=openshift-clusters#next_steps).




## Example commands to create classic clusters
{: #cluster_create_classic}
{: cli}



Classic cluster, shared virtual machine

```sh
ibmcloud oc cluster create classic --name my_cluster --version 4.10_openshift --zone dal10 --flavor b3c.4x16 --hardware shared --workers 3 --public-vlan <public_VLAN_ID> --private-vlan <private_VLAN_ID>
```
{: pre}


Classic cluster, bare metal

```sh
ibmcloud oc cluster create classic --name my_cluster --version 4.10_openshift --zone dal10 --flavor mb2c.4x32 --hardware dedicated --workers 3 --public-vlan <public_VLAN_ID> --private-vlan <private_VLAN_ID>
```
{: pre}



Classic cluster with an IBM Cloud Pak entitlement for a default worker pool of 3 worker nodes with 4 cores and 16 memory each.

```sh
ibmcloud oc cluster create classic --name cloud_pak_cluster --version 4.10_openshift --zone dal10 --flavor b3c.4x16 --hardware dedicated --workers 3 --entitlement cloud_pak --public-vlan <public_VLAN_ID> --private-vlan <private_VLAN_ID> [--operating-system (REDHAT_7_64|REDHAT_8_64)]
```
{: pre}

For a complete list of available RHEL versions and which cluster versions they are compatible with, see [Available {{site.data.keyword.redhat_openshift_notm}} versions](/docs/openshift?topic=openshift-openshift_versions#openshift_versions_available).

```sh
ibmcloud oc cluster create classic --name my_cluster --zone dal10 --flavor b3c.4x16 --version 4.9.28_openshift --operating-system REDHAT_8_64
```




For a classic multizone cluster, after you created the cluster in a [multizone metro](/docs/openshift?topic=openshift-regions-and-zones#zones-mz), [add zones](/docs/openshift?topic=openshift-add_workers#add_zone):
```sh
ibmcloud oc zone add classic --zone <zone> --cluster <cluster_name_or_ID> --worker-pool <pool_name> --private-vlan <private_VLAN_ID> --public-vlan <public_VLAN_ID>
```
{: pre}
