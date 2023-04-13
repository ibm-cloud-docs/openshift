---

copyright: 
  years: 2014, 2023
lastupdated: "2023-04-13"

keywords: openshift, clusters, vpc-gen2

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}






# Creating VPC clusters
{: #cluster-create-vpc-gen2}

[Virtual Private Cloud]{: tag-vpc} 

Use the {{site.data.keyword.cloud_notm}} CLI or the {{site.data.keyword.cloud_notm}} console to create a standard VPC cluster, and customize your cluster to meet the high availability and security requirements of your apps.
{: shortdesc}

Do not delete the subnets that you attach to your cluster during cluster creation or when you add worker nodes in a zone. If you delete a VPC subnet that your cluster used, any load balancers that use IP addresses from the subnet might experience issues, and you might be unable to create new load balancers.
{: important}

## Prerequisites and notes
{: #cluster-create-vpc-prereq}

* If worker nodes must access public endpoints, or if you plan to enable both the public and private cloud service endpoints, you must attach a public gateway to each subnet in your VPC to access default {{site.data.keyword.redhat_openshift_notm}} components such as the web console or OperatorHub.
* If you plan to enable both the public and private cloud service endpoints, you must attach a public gateway to each subnet to access default {{site.data.keyword.redhat_openshift_notm}} components such as the web console or OperatorHub. Additionally, a public network gateway is required when you want your cluster to access public endpoints, such as a public URL of another app or an {{site.data.keyword.cloud_notm}} service that supports public cloud service endpoints only. Make sure to review the [VPC networking basics](/docs/openshift?topic=openshift-plan_vpc_basics) to understand when a public network gateway is required and how you can set up your cluster to limit public access to one or more subnets only.
* Before you can use KMS encryption, you must create a KMS instance and set up the required service authorization in IAM. For more information, see [Managing encryption for the worker nodes in your cluster](/docs/openshift?topic=openshift-encryption#worker-encryption).
* By default, your cluster is provisioned with a VPC security group and a cluster-level security group. If you want to attach additional security groups or change which default security groups are applied when you create the cluster, you must [create your VPC cluster in the CLI](#cluster_vpcg2_cli).
* If you create a VPC cluster with both a public and a private cloud service endpoint, note that the public service endpoints can't be disabled at a later time. Therefore, you can't convert a public cluster to a private cluster. 

## Creating a VPC cluster in the console
{: #clusters_vpcg2_ui}
{: ui}


1. Make sure that you complete the prerequisites to [prepare your account](/docs/containers?topic=containers-clusters&interface=ui) and decide on your cluster setup.
1. [Navigate to the console](https://cloud.ibm.com/kubernetes/catalog/create?platformType=openshift).
1. In the **Infrastructure** section, select **VPC**.
1. In the **Virtual private cloud** section, choose from the following options.
    * Select an existing VPC.
    * Click **Create VPC**.
1. **Optional**: If you selected **Create VPC**, complete the following steps.
    1. Select a **Geography** and **Region**. To review the available regions, see [VPC multizone regions](/docs/openshift?topic=openshift-regions-and-zones#zones-vpc)
    1. Enter a name for your VPC.
    1. Select the **Resource group** where you want to create your VPC.
    1. Enter any tags that you want to associate with your VPC.
    1. Decide whether to **Allow SSH** and **Allow ping** in the default security group.
    1. Decide whether to allow access to Classic resources.
    1. Review the subnet details. By default, subnets are spread evenly across zones. If you want to modify your subnets, uncheck the **Create subnet in every zone** box.
    1. If you modify your subnet details, specify the number of IP addresses to create. VPC subnets provide IP addresses for your worker nodes and load balancer services in the cluster, so [create a VPC subnet with enough IP addresses](/docs/openshift?topic=openshift-vpc-subnets#vpc_basics_subnets). Note that you can't change the number of IPs that a VPC subnet has later. 
    1. If you enter a specific IP range, don't use the following reserved ranges: `172.16.0.0/16`, `172.18.0.0/16`, `172.19.0.0/16`, and `172.20.0.0/16`.
1. Select a standard {{site.data.keyword.cos_full_notm}} instance where a bucket is automatically created for your cluster's internal registry.
1. Select the cluster version.
1. **Optional**: For the **OCP entitlement** section, select an entitlement for a worker pool, if you have one.
    * Usually, select **Purchase additional licenses for this worker pool**. 
    * If you have an {{site.data.keyword.cloud_notm}} Pak with a {{site.data.keyword.redhat_openshift_notm}} entitlement that you want to use, you can select **Apply my Cloud Pak OCP entitlement to this worker pool**. 
    * Later, when you configure the worker pool, make sure to select only the flavor and number of worker nodes that your entitlement permits.
1. Configure the **Location** details for your cluster.
    1. Select the **Resource group** that you want to create your cluster in.
        * A cluster can be created in only one resource group, and after the cluster is created, you can't change its resource group.
        * To create clusters in a resource group other than the default, you must have at least the [**Viewer** role](/docs/openshift?topic=openshift-users#checking-perms) for the resource group.
    2. Select the zones to create your cluster in. For more information about cluster availability, see [Planning your cluster for high availability](/docs/openshift?topic=openshift-ha_clusters).
        * The zones are filtered based on the VPC that you selected, and include the VPC subnets that you previously created.
        * To create a single zone cluster, select one zone only. You can [add zones to your cluster](/docs/openshift?topic=openshift-add_workers#add_zone) later.
        * To create a multizone cluster, select multiple zones.
1. In the **Worker pool** section, choose your worker node flavor and number. You can add more worker pools to your cluster later. To change worker node operating systems, size, or storage, click **Change flavor**.
    * **Default**: The default flavor comes with **4 vCPUs** of computing power and **16 GB** of memory. This virtual flavor is billed hourly. Other types of flavors include the following.
    * **Bare metal**: Bare metal servers are provisioned manually by IBM Cloud infrastructure after you order, and can take more than one business day to complete. Bare metal is best suited for high-performance applications that need more resources and host control. Be sure that you want to provision a bare metal machine. Because it is billed monthly, if you cancel it immediately after an order by mistake, you are still charged the full month.
    * **Virtual - shared**: Infrastructure resources, such as the hypervisor and physical hardware, are shared across you and other IBM customers, but each worker node is accessible only by you. Although this option is usually less expensive and sufficient, you might want to verify your performance and infrastructure requirements with your company policies. Virtual machines are billed hourly.
    * **Virtual - dedicated**: Your worker nodes are hosted on infrastructure that is devoted to your account. Your physical resources are completely isolated. Virtual machines are billed hourly.
1. **Optional**: If the flavor that you want to use has a configurable secondary disk, you can modify the secondary disk by clicking the **Edit** icon ![Edit icon](../icons/edit-tagging.svg "Edit"). Select the storage disks that you want to add to your worker nodes and then click **Apply**. To view a list of VPC worker node flavors and their storage options, see [VPC flavors](/docs/openshift?topic=openshift-vpc-flavors).
1. Set how many worker nodes to create per zone, such as **3**. You must set at least 2 worker nodes. For more information, see [What is the smallest size cluster that I can make?](/docs/openshift?topic=openshift-faqs#smallest_cluster).


1. Configure your cluster with a private or a public and a private cloud service endpoint by setting the **Master service endpoint**. For more information about what setup is required to run internet-facing apps, or to keep your cluster private, see [Planning your cluster network setup](/docs/openshift?topic=openshift-plan_vpc_basics#vpc-workeruser-master).

1. If you don't have the required infrastructure permissions to create a cluster, the **Infrastructure permissions checker** lists the missing permissions. Ask your account owner to [set up the API key](/docs/openshift?topic=openshift-access-creds) with the required permissions.
1. Complete the **Resource details** to customize the unique cluster name and any [tags](/docs/account?topic=account-tag) that you want to use to organize your {{site.data.keyword.cloud_notm}} resources, such as the team or billing department.
1. Enable any integrations that you want to include on your cluster.

    Looking to enable integrations in an existing custer? See [Managing cluster integrations]() for more information. 
    {: tip}

    - [Activity tracking]{: tag-green} Enable the [activity tracking](/docs/activity-tracker?topic=activity-tracker-getting-started) option. From the drop down menu under **Instance**, choose an existing instance or **Create a new instance**. If you choose **Create a new instance**, the details of the new instance are shown. The new instance is created when the cluster is created. If you disable this integration and want to enable it later, see [Getting started with Activity Tracker](/docs/activity-tracker?topic=activity-tracker-getting-started#gs_step2).
    - [Logging]{: tag-dark-teal} Enable the [logging](/docs/log-analysis?topic=log-analysis-getting-started) option. From the drop down **Platform instance** menu, choose a platform instance. From the drop down **Application instance**, choose an existing application instance or choose **Create a new instance**. If you choose **Create a new instance**, the details of the new instance are shown. The new instance is created when the cluster is created. If you disable this integration and want to enable it later, see [Logging for clusters](/docs/openshift?topic=openshift-health&interface=ui).
    - [Monitoring]{: tag-magenta} Enable the [monitoring](/docs/monitoring?topic=monitoring-getting-started) option. From the drop down **Platform instance** menu, choose a platform instance. From the drop down **Application instance**, choose an existing application instance or choose **Create a new instance**. If you choose **Create a new instance**, the details of the new instance are shown. The new instance is created when the cluster is created. If you disable this integration and want to enable it later, see [Monitoring cluster health](/docs/openshift?topic=openshift-health-monitor&interface=ui).
    - [Boot volume encryption]{: tag-blue} Enable [boot volume encryption](/docs/containers?topic=containers-encryption#worker-encryption-vpc). From the drop down menus, select a key management service (KMS) instance and root key to encrypt the local disk for each worker node in the `default` worker pool. 
    - [Secrets Manager]{: tag-teal} Enable [Secrets Manager](/docs/secrets-manager). From the **Secrets Manager instance** drop down menu, choose an existing instance that you want to register to the cluster. If no instances are available, [create one](/docs/containers?topic=containers-secrets-mgr). If you want to apply a secret group, choose one from the **Secrets Manager group** drop down menu. If you disable this integration and want to enable it later, see [About Secrets Manager](/docs/openshift?topic=openshift-secrets-mgr&interface=ui#secrets-mgr_setup).


1. In the **Summary** pane, review the order summary and then click **Create**. A worker pool is created with the number of workers that you specified. You can see the progress of the worker node deployment in the **Worker nodes** tab.
    - Your cluster might take some time to provision the {{site.data.keyword.redhat_openshift_notm}} master and all worker nodes and enter a   **Normal** state. Note that even if the cluster is ready, some parts of the cluster that are used by other services, such as Ingress  secrets or registry image pull secrets, might still be in process. Before you continue, wait until the cluster is ready by checking that the **Ingress subdomain** follows a pattern of `<cluster_name>.<region>.containers.appdomain.cloud`.
    - Every worker node is assigned a unique worker node ID and domain name that must not be changed manually after the cluster is created. Changing the ID or domain name prevents the {{site.data.keyword.redhat_openshift_notm}} master from managing your cluster.
        Is your cluster not in a **Normal** state? Check out the [Debugging clusters](/docs/openshift?topic=openshift-debug_clusters) guide for help. For example, if your cluster is provisioned in an account that is protected by a firewall gateway appliance, you must [configure your firewall settings to allow outgoing traffic to the appropriate ports and IP addresses](/docs/openshift?topic=openshift-firewall#firewall_outbound).
        {: tip}
        
1. After your cluster is created, you can [begin working with your cluster by configuring your CLI session](/docs/openshift?topic=openshift-access_cluster). For more possibilities, review the [Next steps](/docs/openshift?topic=openshift-clusters#next_steps).
1. {{site.data.keyword.redhat_openshift_notm}} version 4.4 or earlier only: To allow any traffic requests to apps that you deploy on your worker nodes, modify the VPC's default security group.
    1. From the [Virtual private cloud dashboard](https://cloud.ibm.com/vpc-ext/network/vpcs){: external}, click the name of the **Default Security Group** for the VPC that you created.
    2. In the **Inbound rules** section, click **New rule**.
    3. Choose the **TCP** protocol, enter `30000` for the **Port min** and `32767` for the **Port max**, and leave the **Any** source type selected.
    4. Click **Save**.
    5. If you require VPC VPN access or classic infrastructure access into this cluster, repeat these steps to add a rule that uses the **UDP** protocol, `30000` for the **Port min**, `32767` for the **Port max**, and the **Any** source type.

## Creating VPC clusters from the CLI
{: #cluster_vpcg2_cli}
{: cli}

Create your single zone or multizone VPC cluster by using the {{site.data.keyword.cloud_notm}} CLI.
{: shortdesc}

**Before you begin**:
* Make sure that you complete the prerequisites to [prepare your account](/docs/containers?topic=containers-clusters&interface=ui) and decide on your cluster setup.
* Install the {{site.data.keyword.cloud_notm}} CLI and the [{{site.data.keyword.openshiftlong_notm}} plug-in](/docs/containers?topic=containers-cs_cli_install#cs_cli_install).
* Install the [VPC CLI plug-in](/docs/vpc?topic=vpc-creating-vpc-resources-with-cli-and-api&interface=cli).


1. In your command line, log in to your {{site.data.keyword.cloud_notm}} account and target the {{site.data.keyword.cloud_notm}} region and resource group where you want to create your VPC cluster. For supported regions, see [Creating a VPC in a different region](/docs/vpc?topic=vpc-creating-a-vpc-in-a-different-region). Enter your {{site.data.keyword.cloud_notm}} credentials when prompted. If you have a federated ID, use the --sso option to log in.
    ```sh
    ibmcloud login -r <region> [-g <resource_group>] [--sso]
    ```
    {: pre}

2. [Create a VPC](/docs/vpc?topic=vpc-creating-vpc-resources-with-cli-and-api&interface=cli#create-a-vpc-cli) in the same region where you want to create the cluster.
    Do the clusters of worker nodes in your VPC need to send and receive information to and from IBM Cloud classic infrastructure? Follow the steps in [Creating VPC subnets for classic access](/docs/openshift?topic=openshift-vpc-subnets#ca_subnet_cli) to create a classic-enabled VPC and VPC subnets without the automatic default address prefixes.
    {: important}
    
3. [Create a subnet for your VPC](/docs/vpc?topic=vpc-creating-vpc-resources-with-cli-and-api&interface=cli#create-a-subnet-cli).
    * If you want to create a [multizone cluster](/docs/openshift?topic=openshift-ha_clusters#mz-clusters), repeat this step to create additional subnets in all the zones that you want to include in your cluster.
    * VPC subnets provide IP addresses for your worker nodes and load balancer services in the cluster, so [create a VPC subnet with enough IP addresses](/docs/openshift?topic=openshift-vpc-subnets#vpc_basics_subnets), such as 256. You can't change the number of IPs that a VPC subnet has later.
    * Do not use the following reserved ranges: `172.16.0.0/16`, `172.18.0.0/16`, `172.19.0.0/16`, and `172.20.0.0/16`.
    * If worker nodes must access public endpoints, or if you plan to enable both the public and private cloud service endpoints, you must [attach a public gateway](/docs/vpc?topic=vpc-creating-vpc-resources-with-cli-and-api&interface=cli#attach-public-gateway-cli) to each subnet to access default {{site.data.keyword.redhat_openshift_notm}} components such as the web console or OperatorHub.
    * **Important**: Do not delete the subnets that you attach to your cluster during cluster creation or when you add worker nodes in a zone. If you delete a VPC subnet that your cluster used, any load balancers that use IP addresses from the subnet might experience issues, and you might be unable to create new load balancers.
    * For more information, see [Overview of VPC networking in {{site.data.keyword.openshiftlong_notm}}: Subnets](/docs/openshift?topic=openshift-vpc-subnets#vpc_basics_subnets).

4. Create the cluster in your VPC. You can use the `ibmcloud oc cluster create vpc-gen2` command to create a single zone cluster in your VPC with worker nodes that are connected to one VPC subnet only. If you want to create a multizone cluster, you can use the {{site.data.keyword.cloud_notm}} console, or [add more zones](/docs/openshift?topic=openshift-add_workers#vpc_add_zone) to your cluster after the cluster is created. The cluster takes a few minutes to provision.
    ```sh
    ibmcloud oc cluster create vpc-gen2 --name <cluster_name> --zone <vpc_zone> --vpc-id <vpc_ID> --subnet-id <vpc_subnet_ID> --flavor <worker_flavor> --version 4.11_openshift --cos-instance <COS_CRN> --workers <number_workers_per_zone> [--sm-group GROUP] [--sm-instance INSTANCE] [--pod-subnet] [--service-subnet] [--disable-public-service-endpoint] [[--kms-account-id <kms_account_ID>] --kms-instance <KMS_instance_ID> --crk <root_key_ID>] [--secondary-storage STORAGE]

    ```
    {: pre}

    `--name <cluster_name>`
    :   Specify a name for your cluster. The name must start with a letter, can contain letters, numbers, periods (.), and hyphen (-), and must be 35 characters or fewer. Use a name that is unique across regions. The cluster name and the region in which the cluster is deployed form the fully qualified domain name for the Ingress subdomain. To ensure that the Ingress subdomain is unique within a region, the cluster name might be truncated and appended with a random value within the Ingress domain name.

    `--zone <zone>`
    :   Specify the {{site.data.keyword.cloud_notm}} zone where you want to create your cluster. Make sure that you use a zone that matches the metro city location that you selected when you created your VPC and that you have an existing VPC subnet for that zone. For example, if you created your VPC in the Dallas metro city, your zone must be set to `us-south-1`, `us-south-2`, or `us-south-3`. To list available VPC cluster zones, run `ibmcloud oc zone ls --provider vpc-gen2`. Note that when you select a zone outside of your country, you might require legal authorization before data can be physically stored in a foreign country.

    `--vpc-id <vpc_ID>`
    :   Enter the ID of the VPC that you created earlier. To retrieve the ID of your VPC, run `ibmcloud oc vpcs`. 

    `--subnet-id <subnet_ID>`
    :   Enter the ID of the VPC subnet that you created earlier. When you create a VPC cluster from the CLI, you can initially create your cluster in one zone with one subnet only. To create a multizone cluster, [add more zones with the subnets](/docs/openshift?topic=openshift-add_workers) that you created earlier to your cluster after the cluster is created. To list the IDs of your subnets in all resource groups, run ` ibmcloud oc subnets --provider vpc-gen2 --vpc-id &lt,VPC_ID> --zone <subnet_zone> `.  

    `--flavor <worker_flavor>`
    :   Enter the worker node flavor that you want to use. The flavor determines the amount of virtual CPU, memory, and disk space that is set up in each worker node and made available to your apps. VPC worker nodes can be created as virtual machines on shared infrastructure only. Bare metal or software-defined storage machines are not supported.  For more information, see [Planning your worker node setup](/docs/openshift?topic=openshift-planning_worker_nodes). To view available flavors, first list available VPC zones with `ibmcloud oc zone ls --provider vpc-gen2`, and then use the zone to list supported flavors by running `ibmcloud oc flavors --zone <VPC_zone> --provider vpc-gen2`. After you create your cluster, you can add different flavors by adding a worker node or worker pool to the cluster.

    `--version 4.11_openshift`
    :   VPC clusters are supported for {{site.data.keyword.redhat_openshift_notm}} version 4 only.
    
    
    `--cos-instance <cos_CRN>`
    :   Include the CRN ID of a standard {{site.data.keyword.cos_full_notm}} instance to back up the internal registry of your cluster. To list the CRN of existing instances, run `ibmcloud resource service-instances --long` and find the **ID** of your object storage instance. To create a standard object storage instance, run `ibmcloud resource service-instance-create <name> cloud-object-storage standard global` and note its **ID**.
    
    
    `--workers <number>`
    :   Specify at least 2 worker nodes to include in the cluster. For more information, see [What is the smallest size cluster that I can make?](/docs/openshift?topic=openshift-faqs#smallest_cluster). This value is optional.

    `--operating-system SYSTEM`
    :   Optional. The operating system of the worker nodes you want to provision in your cluster. For a list of available operating systems by cluster version, see [{{site.data.keyword.openshiftlong_notm}} version information](/docs/openshift?topic=openshift-openshift_versions).
    :   If no option is specified, the default [operating system version that corresponds to the cluster version is used.


   `--cluster-security-group <group_ID>`
    :   Optional. Specify additional security group IDs to apply to all workers on the cluster. You must include a separate `--cluster-security-group` option for each individual security group you want to add. To apply the IBM-created `kube-clusterID`, use `--cluster-security-group cluster`. If no value is specified, only the `kube-clusterID` and the default VPC security group are applied. A maximum of five security groups can be applied to workers, including the default security groups. Note that the VPC security group is only applied if no other security groups are specified. For more information, see [Adding VPC security groups to clusters and worker pools during create time](/docs/containers?topic=containers-vpc-security-group#vpc-sg-cluster).
    
    The security groups applied to a cluster cannot be changed once the cluster is created. You can [change the rules of the security groups](/docs/openshift?topic=openshift-vpc-security-group#vpc-sg-create-rules) that are applied to the cluster, but you cannot add or remove security groups at the cluster level. If you apply the incorrect security groups at cluster create time, you must delete the cluster and create a new one. See [Adding VPC security groups to clusters and worker pools during create time](/docs/containers?topic=containers-vpc-security-group#vpc-sg-cluster) for more details before adding security groups to your cluster. 
    {: important}

    `--sm-group GROUP`
    :    Optional. The secret group ID of the {{site.data.keyword.secrets-manager_short}} instance where your secrets are persisted. To get a secret group ID, see the [{{site.data.keyword.secrets-manager_short}} CLI reference](/docs/secrets-manager-cli-plugin?topic=secrets-manager-cli-plugin-secrets-manager-cli#secrets-manager-secret-groups-cli). Use this option to specify a [secret group](/docs/secrets-manager-cli-plugin?topic=secrets-manager-cli-plugin-secrets-manager-cli#secrets-manager-secret-groups-cli) that controls who on your team has access to cluster secrets. 

    `--sm-instance INSTANCE`
    :    Optional. The CRN of the {{site.data.keyword.secrets-manager_short}} instance. To get the CRN of an instance, run `ibmcloud oc ingress instance ls --cluster CLUSTER`. Include this option if you want to register a {{site.data.keyword.secrets-manager_short}} instance to the cluster.

    `--pod-subnet`
    :   In the first cluster that you create in a VPC, the default pod subnet is `172.17.0.0/18`. In the second cluster that you create in that VPC, the default pod subnet is `172.17.64.0/18`. In each subsequent cluster, the pod subnet range is the next available, non-overlapping `/18` subnet. If you plan to connect your cluster to on-premises networks through {{site.data.keyword.BluDirectLink}} or a VPN service, you can avoid subnet conflicts by specifying a custom subnet CIDR that provides the private IP addresses for your pods.
    When you choose a subnet size, consider the size of the cluster that you plan to create and the number of worker nodes that you might add in the future. The subnet must have a CIDR of at least `/23`, which provides enough pod IP addresses for a maximum of four worker nodes in a cluster. For larger clusters, use `/22` to have enough pod IP addresses for eight worker nodes, `/21` to have enough pod IP addresses for 16 worker nodes, and so on. Note that the pod and service subnets can't overlap. If you use custom-range subnets for your worker nodes, [you must ensure that your worker node subnets don't overlap with your cluster's pod subnet](/docs/openshift?topic=openshift-vpc-subnets#vpc-ip-range). The subnet that you choose must be within one of the following ranges:
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
    - `198.18.0.0 - 198.19.255.255` Note that the pod and service subnets can't overlap.

    `--disable-public-service-endpoint`
    :   Include this option in your command to create your VPC cluster with a private cloud service endpoint only. If you don't include this option, your cluster is set up with a public and a private cloud service endpoint. The service endpoint determines how your {{site.data.keyword.redhat_openshift_notm}} master and the worker nodes communicate, how your cluster access other {{site.data.keyword.cloud_notm}} services and apps outside the cluster, and how your users connect to your cluster. For more information, see [Planning your cluster network setup](/docs/openshift?topic=openshift-plan_clusters).
        If you include this option, your cluster is created with routers and Ingress controllers that expose your apps on the private network only by default. If you later want to expose apps to a public network, you must manually create public routers and Ingress controllers.
        {: important}
        

    `--kms-account-id <KMS_acount_ID>`
    :   Optional: Must be included if the `--kms-instance-id` and `--crk` options are provided and the KMS instance resides in an account different from the cluster's account, otherwise it can be omitted.
        Setting up encryption by using a KMS from a different account is available for allowlisted accounts only. To get added to the allowlist, [open a case](https://cloud.ibm.com/unifiedsupport/cases/form){: external} with support.
        {: note}


    `--kms-instance <KMS_instance_ID>`
    :   Optional: Include the ID of a key management service (KMS) instance to use to encrypt the local disk on the worker nodes in the `default` worker pool. To list available KMS instances, run `ibmcloud oc kms instance ls`. If you include this option, you must also include the `--crk` option.
        Before you can use KMS encryption, you must create a KMS instance and set up the required service authorization in IAM. See [Managing encryption](/docs/openshift?topic=openshift-encryption#worker-encryption) for the worker nodes in your cluster.
        {: note}
  

    `--crk <root_key>`
    :   Optional: Include the ID of the root key in the KMS instance to use to encrypt the local disk on the worker nodes in the `default` worker pool. To list available root keys, run `ibmcloud oc kms crk ls --instance-id`. If you include this option, you must also include the `--kms-instance` option.
        Before you can use KMS encryption, you must create a KMS instance and set up the required service authorization in IAM. See [Managing encryption](/docs/openshift?topic=openshift-encryption#worker-encryption) for the worker nodes in your cluster.
        {: note}

    `--secondary-storage STORAGE`
    :    Optional. The storage option for the flavor. For example, `900gb.5iops-tier`. When you add a secondary disk, that disk is used for the container runtime, while the primary disk is used for the operating system. To view the storage options for a flavor, run the `**ibmcloud oc flavor get --flavor FLAVOR --zone ZONE --provider vpc-gen2` command. To view a list of VPC worker node flavors, see [VPC flavors](/docs/openshift?topic=openshift-vpc-flavors&interface=ui)
    
5. Verify that the creation of the cluster was requested. It can take a few minutes for the worker node machines to be ordered, and for the cluster to be set up and provisioned in your account.
    ```sh
    ibmcloud oc cluster ls
    ```
    {: pre}

    When the provisioning of your {{site.data.keyword.redhat_openshift_notm}} master is completed, the state of your cluster changes to **normal**. After the {{site.data.keyword.redhat_openshift_notm}} master is ready, your worker nodes are set up.
    ```sh
    NAME         ID                                   State      Created          Workers    Zone      Version     Resource Group Name   Provider
    mycluster    aaf97a8843a29941b49a598f516da72101   normal   20170201162433   3          Dallas     4.11.31_1544_openshift      Default               vpc-gen2
    ```
    {: screen}

    Is your cluster not in a **normal** state? Check out the [Debugging clusters](/docs/openshift?topic=openshift-debug_clusters) guide for help. For example, if your cluster is provisioned in an account that is protected by a firewall gateway appliance, you must [configure your firewall settings to allow outgoing traffic to the appropriate ports and IP addresses](/docs/openshift?topic=openshift-firewall#firewall_outbound).
    {: tip}

6. Check the status of the worker nodes.
    ```sh
    ibmcloud oc worker ls --cluster <cluster_name_or_ID>
    ```
    {: pre}

    When the worker nodes are ready, the worker node **State** changes to `normal` and the **Status** changes to `Ready`. When the node **Status** changes to `Ready`, you can access the cluster. Note that even if the cluster is ready, some parts of the cluster that are used by other services, such as Ingress secrets or registry image pull secrets, might still be in process.
    ```sh
    ID                                                     Public IP        Private IP     Flavor              State    Status   Zone    Version
    kube-blrs3b1d0p0p2f7haq0g-mycluster-default-000001f7   169.xx.xxx.xxx  10.xxx.xx.xxx   b3c.4x16.encrypted  normal   Ready    dal10   4.11.31_1544_openshift
    ```
    {: screen}

    Every worker node is assigned a unique worker node ID and domain name that must not be changed manually after the cluster is created. If you change the ID or domain name, the {{site.data.keyword.redhat_openshift_notm}} master cannot manage your cluster.
    {: important}

Your cluster is ready for your workloads! You might also want to [add a tag to your cluster](/docs/openshift?topic=openshift-add_workers#cluster_tags), such as the team or billing department that uses the cluster, to help manage {{site.data.keyword.cloud_notm}} resources. For more ideas of what to do with your cluster, review the [Next steps](/docs/openshift?topic=openshift-clusters#next_steps). 


## Example commands to create VPC clusters
{: #cluster_create_vpc}
{: cli}

VPC Gen 2 cluster flavors with instance storage are available for allowlisted accounts. To get added to the allowlist, [open a case](https://cloud.ibm.com/unifiedsupport/cases/form){: external} with support.
{: note}

```sh
ibmcloud oc cluster create vpc-gen2 --name my_cluster --version 4.11_openshift --zone us-east-1 --vpc-id <VPC_ID> --subnet-id <VPC_SUBNET_ID> --cos-instance <COS_CRN>--flavor b2.4x16 --workers 3
```
{: pre}

For a VPC multizone cluster, after you created the cluster in a [multizone metro](/docs/openshift?topic=openshift-regions-and-zones#zones-vpc), [add zones](/docs/openshift?topic=openshift-add_workers#vpc_add_zone).

```sh
ibmcloud oc zone add vpc-gen2 --zone <zone> --cluster <cluster_name_or_ID> --worker-pool <pool_name> --subnet-id <VPC_SUBNET_ID>
```
{: pre}

VPC cluster provisioned at version 4.9 with worker nodes that run the RHEL 8 operating system. For a complete list of available RHEL versions and which cluster versions they are compatible with, see [Available {{site.data.keyword.redhat_openshift_notm}} versions](/docs/openshift?topic=openshift-openshift_versions#openshift_versions_available).

```sh
ibmcloud oc cluster create vpc-gen2 --name my_cluster --zone us-south-1 --flavor b3c.4x16 --vpc_ID <vpc_id> --subnet-id <vpc_subnet_id> --version 4.9.28_openshift --operating-system REDHAT_8_64
```
{: pre}



