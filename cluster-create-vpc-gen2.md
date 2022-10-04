---

copyright: 
  years: 2014, 2022
lastupdated: "2022-10-04"

keywords: openshift, clusters, vpc-gen2

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}




# Creating VPC Gen 2 clusters
{: #cluster-create-vpc-gen2}

Use the {{site.data.keyword.cloud_notm}} CLI or the {{site.data.keyword.cloud_notm}} console to create a standard VPC cluster, and customize your cluster to meet the high availability and security requirements of your apps.
{: shortdesc}

## Creating a standard VPC cluster in the console
{: #clusters_vpcg2_ui}
{: ui}

Create your single zone or multizone VPC cluster by using the {{site.data.keyword.cloud_notm}} console.
{: shortdesc}

By default, your cluster is provisioned with a VPC security group and a cluster-level security group. If you want to attach additional security groups or change which default security groups are applied when you create the cluster, you must [create your VPC cluster in the CLI](#cluster_vpcg2_cli).
{: tip}



Your VPC cluster is created with both a public and a private cloud service endpoint. Public service endpoints can't later be disabled, and therefore, you can't convert a public cluster to a private cluster. 
{: important}



1. Make sure that you complete the prerequisites to [prepare your account](#cluster_prepare) and decide on your [cluster setup](#prepare_cluster_level).
1. [Create a Virtual Private Cloud (VPC) on generation 2 compute](https://cloud.ibm.com/vpc/provision/vpc){: external} with a subnet that is located in the VPC zone where you want to create the cluster.
    * During the VPC creation, three subnets are created by default. Subnets are specific to a zone. If you want to create a multizone cluster, create the subnet in one of the multizone-capable zones that you want to use. Later, you manually create the subnets for the remaining zones that you want to include in your cluster.
    
        Do not delete the subnets that you attach to your cluster during cluster creation or when you add worker nodes in a zone. If you delete a VPC subnet that your cluster used, any load balancers that use IP addresses from the subnet might experience issues, and you might be unable to create new load balancers.
        {: important}
        
        
    * If worker nodes must access public endpoints, or if you plan to enable both the public and private cloud service endpoints, you must attach a public gateway to each subnet to access default {{site.data.keyword.redhat_openshift_notm}} components such as the web console or OperatorHub.
    * If you require access to classic infrastructure resources, you must follow the steps in [Creating VPC subnets for classic access](/docs/containers?topic=containers-vpc-subnets#ca_subnet_ui) to create a classic access VPC and VPC subnets without the automatic default address prefixes.
    * For more information, see [Creating a VPC using the IBM Cloud console](/docs/vpc?topic=vpc-creating-a-vpc-using-the-ibm-cloud-console) and [Overview of VPC networking in {{site.data.keyword.openshiftlong_notm}}: Subnets](/docs/containers?topic=containers-vpc-subnets#vpc_basics_subnets).

1. If you want to create a multizone cluster, create the subnets for all the remaining zones that you want to include in your cluster. You must have one VPC subnet in all the zones where you want to create your multizone cluster.
    1. From the [VPC subnet dashboard](https://cloud.ibm.com/vpc/network/subnets){: external}, click **New subnet**.
    2. Enter a name for your subnet.
    3. Select the location of your VPC and zone where you want to create the subnet.
    4. Select the name of the VPC that you created.
    5. Specify the number of IP addresses to create. VPC subnets provide IP addresses for your worker nodes and load balancer services in the cluster, so [create a VPC subnet with enough IP addresses](/docs/containers?topic=containers-vpc-subnets#vpc_basics_subnets), such as 256. You can't change the number of IPs that a VPC subnet has later. If you enter a specific IP range, don't use the following reserved ranges: `172.16.0.0/16`, `172.18.0.0/16`, `172.19.0.0/16`, and `172.20.0.0/16`.
    6. Choose if you want to attach a public network gateway to your subnet. If you plan to enable both the public and private cloud service endpoints, you must attach a public gateway to each subnet to access default {{site.data.keyword.redhat_openshift_notm}} components such as the web console or OperatorHub. Additionally, a public network gateway is required when you want your cluster to access public endpoints, such as a public URL of another app or an {{site.data.keyword.cloud_notm}} service that supports public cloud service endpoints only. Make sure to review the [VPC networking basics](/docs/containers?topic=containers-plan_vpc_basics) to understand when a public network gateway is required and how you can set up your cluster to limit public access to one or more subnets only.
    7. Click **Create subnet**.
1. From the [{{site.data.keyword.redhat_openshift_notm}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, click **Create cluster**.
1. Configure your cluster environment.
    1. Select the **Standard** cluster plan.
    1. From the {{site.data.keyword.redhat_openshift_notm}} drop-down list, select the version that you want to use in your cluster.
    1. **Optional**: For the **OCP entitlement** section, you can select an entitlement for a worker pool, if you have one. Usually, leave the value set to **Purchase additional licenses for this worker pool**. If you have an {{site.data.keyword.cloud_notm}} Pak with a {{site.data.keyword.redhat_openshift_notm}} entitlement that you want to use, you can select **Apply my Cloud Pak OCP entitlement to this worker pool**. Later, when you configure the worker pool, make sure to select only the flavor and number of worker nodes that your entitlement permits.
    1. Select **VPC** infrastructure.
    1. From the **Virtual private cloud** drop-down menu, select the VPC that you created earlier.
1. Configure the **Location** details for your cluster.
    1. Select the **Resource group** that you want to create your cluster in.
        * A cluster can be created in only one resource group, and after the cluster is created, you can't change its resource group.
        * To create clusters in a resource group other than the default, you must have at least the [**Viewer** role](/docs/containers?topic=containers-users#checking-perms) for the resource group.
    2. Select the zones to create your cluster in.
        * The zones are filtered based on the VPC that you selected, and include the VPC subnets that you previously created.
        * To create a [single zone cluster](/docs/containers?topic=containers-ha_clusters#single_zone), select one zone only. If you select only one zone, you can [add zones to your cluster](/docs/containers?topic=containers-add_workers#add_zone) after the cluster is created.
        * To create a [multizone cluster](/docs/containers?topic=containers-ha_clusters#multizone), select multiple zones.
1. Configure your **Worker pool** setup. Worker pools are groups of worker nodes that share the same configuration. You can always add more worker pools to your cluster later.
    1. If you want a larger size for your worker nodes, or if you want to change worker node operating systems, click **Change flavor**. The flavor defines the amount of virtual CPU, memory, and disk space that is set up in each worker node and made available to the containers. Available bare metal and virtual machines types vary by the zone in which you deploy the cluster. For more information, see [Planning your worker node setup](/docs/containers?topic=containers-planning_worker_nodes). After you create your cluster, you can add different flavors by adding a worker pool to the cluster.
        * **Default**: The default flavor comes with **4 vCPUs** of computing power and **16 GB** of memory. This virtual flavor is billed hourly. Other types of flavors include the following.
        * **Bare metal**: Bare metal servers are provisioned manually by IBM Cloud infrastructure after you order, and can take more than one business day to complete. Bare metal is best suited for high-performance applications that need more resources and host control. Be sure that you want to provision a bare metal machine. Because it is billed monthly, if you cancel it immediately after an order by mistake, you are still charged the full month.
        * **Virtual - shared**: Infrastructure resources, such as the hypervisor and physical hardware, are shared across you and other IBM customers, but each worker node is accessible only by you. Although this option is less expensive and sufficient in most cases, you might want to verify your performance and infrastructure requirements with your company policies. Virtual machines are billed hourly.
        * **Virtual - dedicated**: Your worker nodes are hosted on infrastructure that is devoted to your account. Your physical resources are completely isolated. Virtual machines are billed hourly.
    2. Set how many worker nodes to create per zone, such as **3**. For example, if you selected 2 zones and want to create 3 worker nodes, a total of 6 worker nodes are provisioned in your cluster with 3 worker nodes in each zone. You must set at least 2 worker nodes. For more information, see [What is the smallest size cluster that I can make?](/docs/containers?topic=containers-faqs#smallest_cluster).
    3. Select a key management service (KMS) instance and root key to encrypt the local disk for each worker node in the `default` worker pool.

    Before you can use KMS encryption, you must create a KMS instance and set up the required service authorization in IAM. See [Managing encryption for the worker nodes in your cluster](/docs/containers?topic=containers-encryption#worker-encryption).
    {: note}

1. If you don't have the required infrastructure permissions to create a cluster, the **Infrastructure permissions checker** lists the missing permissions. Ask your account owner to [set up the API key](/docs/containers?topic=containers-access-creds) with the required permissions.
1. Complete the **Resource details** to customize the unique cluster name and any [tags](/docs/account?topic=account-tag) that you want to use to organize your {{site.data.keyword.cloud_notm}} resources, such as the team or billing department.
1. In the **Summary** pane, review the order summary and then click **Create**. A worker pool is created with the number of workers that you specified. You can see the progress of the worker node deployment in the **Worker nodes** tab.
    - Your cluster might take some time to provision the {{site.data.keyword.redhat_openshift_notm}} master and all worker nodes and enter a   **Normal** state. Note that even if the cluster is ready, some parts of the cluster that are used by other services, such as Ingress  secrets or registry image pull secrets, might still be in process. Before you continue, wait until the cluster is ready by checking that the **Ingress subdomain** follows a pattern of `<cluster_name>.<region>.containers.appdomain.cloud`.
    - Every worker node is assigned a unique worker node ID and domain name that must not be changed manually after the cluster is created. Changing the ID or domain name prevents the {{site.data.keyword.redhat_openshift_notm}} master from managing your cluster.
        Is your cluster not in a **Normal** state? Check out the [Debugging clusters](/docs/containers?topic=containers-debug_clusters) guide for help. For example, if your cluster is provisioned in an account that is protected by a firewall gateway appliance, you must [configure your firewall settings to allow outgoing traffic to the appropriate ports and IP addresses](/docs/containers?topic=containers-firewall#firewall_outbound).
        {: tip}
        
1. After your cluster is created, you can [begin working with your cluster by configuring your CLI session](/docs/openshift?topic=openshift-access_cluster). For more possibilities, review the [Next steps](/docs/containers?topic=containers-clusters#next_steps).
1. {{site.data.keyword.redhat_openshift_notm}} version 4.4 or earlier only: To allow any traffic requests to apps that you deploy on your worker nodes, modify the VPC's default security group.
    1. From the [Virtual private cloud dashboard](https://cloud.ibm.com/vpc-ext/network/vpcs){: external}, click the name of the **Default Security Group** for the VPC that you created.
    2. In the **Inbound rules** section, click **New rule**.
    3. Choose the **TCP** protocol, enter `30000` for the **Port min** and `32767` for the **Port max**, and leave the **Any** source type selected.
    4. Click **Save**.
    5. If you require VPC VPN access or classic infrastructure access into this cluster, repeat these steps to add a rule that uses the **UDP** protocol, `30000` for the **Port min**, `32767` for the **Port max**, and the **Any** source type.

## Creating standard VPC clusters from the CLI
{: #cluster_vpcg2_cli}
{: cli}

Create your single zone or multizone VPC cluster by using the {{site.data.keyword.cloud_notm}} CLI.
{: shortdesc}

**Before you begin**:
* Make sure that you complete the prerequisites to [prepare your account](#cluster_prepare) and decide on your [cluster setup](#prepare_cluster_level).
* Install the {{site.data.keyword.cloud_notm}} CLI and the [{{site.data.keyword.openshiftlong_notm}} plug-in](/docs/containers?topic=containers-cs_cli_install#cs_cli_install).
* Install the [VPC CLI plug-in](/docs/vpc?topic=vpc-infrastructure-cli-plugin-vpc-reference#cli-ref-prereqs).


1. In your command line, log in to your {{site.data.keyword.cloud_notm}} account and target the {{site.data.keyword.cloud_notm}} region and resource group where you want to create your VPC cluster. For supported regions, see [Creating a VPC in a different region](/docs/vpc?topic=vpc-creating-a-vpc-in-a-different-region). Enter your {{site.data.keyword.cloud_notm}} credentials when prompted. If you have a federated ID, use the --sso flag to log in.
    ```sh
    ibmcloud login -r <region> [-g <resource_group>] [--sso]
    ```
    {: pre}

2. [Create a VPC](/docs/vpc?topic=vpc-creating-vpc-resources-with-cli-and-api&interface=cli#create-a-vpc-cli) in the same region where you want to create the cluster.
    Do the clusters of worker nodes in your VPC need to send and receive information to and from IBM Cloud classic infrastructure? Follow the steps in [Creating VPC subnets for classic access](/docs/containers?topic=containers-vpc-subnets#ca_subnet_cli) to create a classic-enabled VPC and VPC subnets without the automatic default address prefixes.
    {: important}
    
3. [Create a subnet for your VPC](/docs/vpc?topic=vpc-creating-vpc-resources-with-cli-and-api&interface=cli#create-a-subnet-cli).
    * If you want to create a [multizone cluster](/docs/containers?topic=containers-ha_clusters#multizone), repeat this step to create additional subnets in all the zones that you want to include in your cluster.
    * VPC subnets provide IP addresses for your worker nodes and load balancer services in the cluster, so [create a VPC subnet with enough IP addresses](/docs/containers?topic=containers-vpc-subnets#vpc_basics_subnets), such as 256. You can't change the number of IPs that a VPC subnet has later.
    * Do not use the following reserved ranges: `172.16.0.0/16`, `172.18.0.0/16`, `172.19.0.0/16`, and `172.20.0.0/16`.
    * If worker nodes must access public endpoints, or if you plan to enable both the public and private cloud service endpoints, you must [attach a public gateway](/docs/vpc?topic=vpc-creating-vpc-resources-with-cli-and-api&interface=cli#attach-public-gateway-cli) to each subnet to access default {{site.data.keyword.redhat_openshift_notm}} components such as the web console or OperatorHub.
    * **Important**: Do not delete the subnets that you attach to your cluster during cluster creation or when you add worker nodes in a zone. If you delete a VPC subnet that your cluster used, any load balancers that use IP addresses from the subnet might experience issues, and you might be unable to create new load balancers.
    * For more information, see [Overview of VPC networking in {{site.data.keyword.openshiftlong_notm}}: Subnets](/docs/containers?topic=containers-vpc-subnets#vpc_basics_subnets).

4. Create the cluster in your VPC. You can use the `ibmcloud oc cluster create vpc-gen2` command to create a single zone cluster in your VPC with worker nodes that are connected to one VPC subnet only. If you want to create a multizone cluster, you can use the {{site.data.keyword.cloud_notm}} console, or [add more zones](/docs/containers?topic=containers-add_workers#vpc_add_zone) to your cluster after the cluster is created. The cluster takes a few minutes to provision.
    ```sh
    ibmcloud oc cluster create vpc-gen2 --name <cluster_name> --zone <vpc_zone> --vpc-id <vpc_ID> --subnet-id <vpc_subnet_ID> --flavor <worker_flavor> --version 4.9_openshift --cos-instance <COS_CRN> --workers <number_workers_per_zone> [--sm-group GROUP] [--sm-instance INSTANCE] [--pod-subnet] [--service-subnet] [--disable-public-service-endpoint] [[--kms-account-id <kms_account_ID>] --kms-instance <KMS_instance_ID> --crk <root_key_ID>] 

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

    `--version 4.9_openshift`
    :   VPC clusters are supported for {{site.data.keyword.redhat_openshift_notm}} version 4 only.
    
    
    `--cos-instance <cos_CRN>`
    :   Include the CRN ID of a standard {{site.data.keyword.cos_full_notm}} instance to back up the internal registry of your cluster. To list the CRN of existing instances, run `ibmcloud resource service-instances --long` and find the **ID** of your object storage instance. To create a standard object storage instance, run `ibmcloud resource service-instance-create <name> cloud-object-storage standard global` and note its **ID**.
    
    
    `--workers <number>`
    :   Specify at least 2 worker nodes to include in the cluster. For more information, see [What is the smallest size cluster that I can make?](/docs/containers?topic=containers-faqs#smallest_cluster). This value is optional.

    :   If no option is specified, the default [operating system version that corresponds to the cluster version](/docs/openshift?topic=openshift-openshift_versions#openshift_versions_available) is used.


   `--cluster-security-group <group_ID>`
    :   Optional. Specify additional security group IDs to apply to all workers on the cluster. You must include a separate `--cluster-security-group` option for each individual security group you want to add. To apply the IBM-created `kube-clusterID`, use `--cluster-security-group cluster`. If no value is specified, only the `kube-clusterID` and the default VPC security group are applied. A maximum of five security groups can be applied to workers, including the default security groups. Note that the VPC security group is only applied if no other security groups are specified. For more information, see [Adding VPC security groups to clusters and worker pools during create time](/docs/containers?topic=containers-vpc-security-group#vpc-sg-cluster).
    
    The security groups applied to a cluster cannot be changed once the cluster is created. You can [change the rules of the security groups](/docs/containers?topic=containers-vpc-security-group#vpc-sg-create-rules) that are applied to the cluster, but you cannot add or remove security groups at the cluster level. If you apply the incorrect security groups at cluster create time, you must delete the cluster and create a new one. See [Adding VPC security groups to clusters and worker pools during create time](/docs/containers?topic=containers-vpc-security-group#vpc-sg-cluster) for more details before adding security groups to your cluster. 
    {: important}

    `--sm-group GROUP`
    :    Optional. The secret group ID of the {{site.data.keyword.secrets-manager_short}} instance where your secrets are persisted. To get a secret group ID, see the [{{site.data.keyword.secrets-manager_short}} CLI reference](/docs/secrets-manager?topic=secrets-manager-cli-plugin-secrets-manager-cli#secrets-manager-cli-secret-groups-command). Use this option to specify a [secret group](/docs/secrets-manager?topic=secrets-manager-cli-plugin-secrets-manager-cli#secrets-manager-secret-groups-cli) that controls who on your team has access to cluster secrets. 

    `--sm-instance INSTANCE`
    :    Optional. The CRN of the {{site.data.keyword.secrets-manager_short}} instance. To get the CRN of an instance, run `ibmcloud oc ingress instance ls --cluster CLUSTER`. Include this option if you want to register a {{site.data.keyword.secrets-manager_short}} instance to the cluster.

    `--pod-subnet`
    :   In the first cluster that you create in a VPC, the default pod subnet is `172.17.0.0/18`. In the second cluster that you create in that VPC, the default pod subnet is `172.17.64.0/18`. In each subsequent cluster, the pod subnet range is the next available, non-overlapping `/18` subnet. If you plan to connect your cluster to on-premises networks through {{site.data.keyword.BluDirectLink}} or a VPN service, you can avoid subnet conflicts by specifying a custom subnet CIDR that provides the private IP addresses for your pods.
    When you choose a subnet size, consider the size of the cluster that you plan to create and the number of worker nodes that you might add in the future. The subnet must have a CIDR of at least `/23`, which provides enough pod IP addresses for a maximum of four worker nodes in a cluster. For larger clusters, use `/22` to have enough pod IP addresses for eight worker nodes, `/21` to have enough pod IP addresses for 16 worker nodes, and so on. Note that the pod and service subnets can't overlap. If you use custom-range subnets for your worker nodes, [you must ensure that your worker node subnets don't overlap with your cluster's pod subnet](/docs/containers?topic=containers-vpc-subnets#vpc-ip-range). The subnet that you choose must be within one of the following ranges:
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
    :   Include this option in your command to create your VPC cluster with a private cloud service endpoint only. If you don't include this option, your cluster is set up with a public and a private cloud service endpoint. The service endpoint determines how your {{site.data.keyword.redhat_openshift_notm}} master and the worker nodes communicate, how your cluster access other {{site.data.keyword.cloud_notm}} services and apps outside the cluster, and how your users connect to your cluster. For more information, see [Planning your cluster network setup](/docs/containers?topic=containers-plan_clusters).
        If you include this flag, your cluster is created with routers and Ingress controllers that expose your apps on the private network only by default. If you later want to expose apps to a public network, you must manually create public routers and Ingress controllers.
        {: important}
        

    `--kms-account-id <KMS_acount_ID>`
    :   Optional: Must be included if the `--kms-instance-id` and `--crk` flags are provided and the KMS instance resides in an account different from the cluster's account, otherwise it can be omitted.
        Setting up encryption by using a KMS from a different account is available for allowlisted accounts only. To get added to the allowlist, [open a case](https://cloud.ibm.com/unifiedsupport/cases/form){: external} with support.
        {: note}


    `--kms-instance <KMS_instance_ID>`
    :   Optional: Include the ID of a key management service (KMS) instance to use to encrypt the local disk on the worker nodes in the `default` worker pool. To list available KMS instances, run `ibmcloud oc kms instance ls`. If you include this option, you must also include the `--crk` option.
        Before you can use KMS encryption, you must create a KMS instance and set up the required service authorization in IAM. See [Managing encryption](/docs/containers?topic=containers-encryption#worker-encryption) for the worker nodes in your cluster.
        {: note}
  

    `--crk <root_key>`
    :   Optional: Include the ID of the root key in the KMS instance to use to encrypt the local disk on the worker nodes in the `default` worker pool. To list available root keys, run `ibmcloud oc kms crk ls --instance-id`. If you include this option, you must also include the `--kms-instance` option.
        Before you can use KMS encryption, you must create a KMS instance and set up the required service authorization in IAM. See [Managing encryption](/docs/containers?topic=containers-encryption#worker-encryption) for the worker nodes in your cluster.
        {: note}
    
5. Verify that the creation of the cluster was requested. It can take a few minutes for the worker node machines to be ordered, and for the cluster to be set up and provisioned in your account.
    ```sh
    ibmcloud oc cluster ls
    ```
    {: pre}

    When the provisioning of your {{site.data.keyword.redhat_openshift_notm}} master is completed, the state of your cluster changes to **normal**. After the {{site.data.keyword.redhat_openshift_notm}} master is ready, your worker nodes are set up.
    ```sh
    NAME         ID                                   State      Created          Workers    Zone      Version     Resource Group Name   Provider
    mycluster    aaf97a8843a29941b49a598f516da72101   normal   20170201162433   3          Dallas     4.9.46_1544_openshift      Default               vpc-gen2
    ```
    {: screen}

    Is your cluster not in a **normal** state? Check out the [Debugging clusters](/docs/containers?topic=containers-debug_clusters) guide for help. For example, if your cluster is provisioned in an account that is protected by a firewall gateway appliance, you must [configure your firewall settings to allow outgoing traffic to the appropriate ports and IP addresses](/docs/containers?topic=containers-firewall#firewall_outbound).
    {: tip}

6. Check the status of the worker nodes.
    ```sh
    ibmcloud oc worker ls --cluster <cluster_name_or_ID>
    ```
    {: pre}

    When the worker nodes are ready, the worker node **State** changes to `normal` and the **Status** changes to `Ready`. When the node **Status** changes to `Ready`, you can access the cluster. Note that even if the cluster is ready, some parts of the cluster that are used by other services, such as Ingress secrets or registry image pull secrets, might still be in process.
    ```sh
    ID                                                     Public IP        Private IP     Flavor              State    Status   Zone    Version
    kube-blrs3b1d0p0p2f7haq0g-mycluster-default-000001f7   169.xx.xxx.xxx  10.xxx.xx.xxx   b3c.4x16.encrypted  normal   Ready    dal10   4.9.46_1544_openshift
    ```
    {: screen}

    Every worker node is assigned a unique worker node ID and domain name that must not be changed manually after the cluster is created. If you change the ID or domain name, the {{site.data.keyword.redhat_openshift_notm}} master cannot manage your cluster.
    {: important}

7. **Optional**: If you created your cluster in a [multizone metro location](/docs/containers?topic=containers-regions-and-zones#zones-vpc), you can [spread the default worker pool across zones](/docs/containers?topic=containers-add_workers#vpc_add_zone) to increase the cluster's availability.

8. After your cluster is created, you can [begin working with your cluster by configuring your CLI session](/docs/openshift?topic=openshift-access_cluster).

9. {{site.data.keyword.redhat_openshift_notm}} version 4.4 or earlier only: To allow any traffic requests to apps that you deploy on your worker nodes, you can modify the VPC's default security group. 

    If you modify the default VPC security group, you must make sure that the [minimum traffic rules](/docs/containers?topic=containers-vpc-security-group#required-group-rules-workers) are still covered.
    {: note}

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

Your cluster is ready for your workloads! You might also want to [add a tag to your cluster](/docs/containers?topic=containers-add_workers#cluster_tags), such as the team or billing department that uses the cluster, to help manage {{site.data.keyword.cloud_notm}} resources. For more ideas of what to do with your cluster, review the [Next steps](/docs/containers?topic=containers-clusters#next_steps). 


## Example commands to create VPC clusters
{: #cluster_create_vpc}
{: cli}

VPC Gen 2 cluster flavors with instance storage are available for allowlisted accounts. To get added to the allowlist, [open a case](https://cloud.ibm.com/unifiedsupport/cases/form){: external} with support.
{: note}

```sh
ibmcloud oc cluster create vpc-gen2 --name my_cluster --version 4.9_openshift --zone us-east-1 --vpc-id <VPC_ID> --subnet-id <VPC_SUBNET_ID> --cos-instance <COS_CRN>--flavor b2.4x16 --workers 3
```
{: pre}

For a VPC multizone cluster, after you created the cluster in a [multizone metro](/docs/containers?topic=containers-regions-and-zones#zones-vpc), [add zones](/docs/containers?topic=containers-add_workers#vpc_add_zone).

```sh
ibmcloud oc zone add vpc-gen2 --zone <zone> --cluster <cluster_name_or_ID> --worker-pool <pool_name> --subnet-id <VPC_SUBNET_ID>
```
{: pre}

