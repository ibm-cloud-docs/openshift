---

copyright: 
  years: 2014, 2025
lastupdated: "2025-08-07"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, kubernetes, clusters, worker nodes, worker pools, classic, create

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}

# Creating classic clusters
{: #cluster-create-classic}

[Classic infrastructure]{: tag-classic-inf}


Use the {{site.data.keyword.cloud_notm}} CLI or the {{site.data.keyword.cloud_notm}} console to create a fully customizable standard cluster with your choice of hardware isolation and access to features like multiple worker nodes for a highly available environment.
{: shortdesc}

## Prerequisites
{: #classic-cluster-prereqs}

{{site.data.keyword.redhat_openshift_notm}} clusters can be created created with a public only or both a public and private service endpoint. Public service endpoints can't be disabled. Therefore, you can't convert a public {{site.data.keyword.redhat_openshift_notm}} cluster to a private one. If you want to create a Classic cluster with a private service endpoint enabled, you must [enable VRF](/docs/account?topic=account-vrf-service-endpoint&interface=ui#vrf) & [service endpoints](/docs/account?topic=account-vrf-service-endpoint&interface=ui#service-endpoint). If you want a private-only cluster, consider creating a VPC cluster.
{: important}




## Creating a classic cluster in the console
{: #clusters_ui}
{: ui}

To begin creating your cluster, navigate to the [console](https://cloud.ibm.com/containers/cluster-management/clusters){: external} and click **Create cluster**.
{: shortdesc}


Location details
:    When you create a cluster, its resources remain in the location that you deploy the cluster to.
:    - **Resource group**: A cluster can be created in only one resource group, and after the cluster is created, you can't change its resource group. To create clusters in a resource group other than the default, you must have at least the [**Viewer** role](/docs/openshift?topic=openshift-iam-platform-access-roles) for the resource group.
:    - **Geography**: Select an area to create the cluster in, such as **North America**. The geography helps filter the **Availability** and **Metro** values that you can select in the console.
:    - **Availability**: A cluster can be created with a **Single zone** or **Multizone** configuration. A multizone cluster provides high availability, with the {{site.data.keyword.redhat_openshift_notm}} master deployed in a multizone-capable zone and three replicas of the master spread across different zones.
        - For multizone clusters, choose a **Metro** location. For the best performance, select the region that is physically closest to you. Your **Worker zones** are based on the region you choose. You can select which worker zones to apply, and your worker nodes are spread across your zones for high availability. Each worker zone has a public and private **VLAN**. If you do not have VLANs in that zone, they are created for you. 
        - For single zone clusters, choose a single **Worker zone** to host your cluster in. For the best performance, select a zone in the city that is physically closest to you. Each worker zone has a public and private **VLAN**. If you do not have a VLANs in that zone, they are created for you.

Kubernetes version
:    By default, clusters are created with the default Kubernetes version. You can specify a different [supported version](/docs/containers?topic=containers-cs_versions#cs_versions_available). 

Worker pool
:    The cluster worker pool defines the number and type of worker nodes that run your workload. You can change your worker pool details at anytime.
:    - **Flavor**: The flavor defines the amount of virtual CPU, memory, and disk space that is set up in each worker node and made available to the containers. Available bare metal and virtual machines types vary by the zone in which you deploy the cluster. 
:    - **Operating system** and **Architecture**:  For a list of the available operating systems and architectures by cluster version, see the [available versions](/docs/containers?topic=containers-cs_versions#cs_versions_available).
:    - **Worker nodes per zone**: For high availability, at least 3 worker nodes per zone are recommended. 
:    - **Encrypt local disk**: By default, [worker nodes feature AES 256-bit disk encryption](/docs/openshift?topic=openshift-security#workernodes). You can choose to turn off disk encryption when you create the cluster.


Master service endpoint
:    Service endpoints provide communication to the master. You can choose to configure your cluster with a public only or both a public and a private cloud service endpoint. For more information about what setup is required to run internet-facing apps, or to keep your cluster private, see [Planning your cluster network setup](/docs/containers?topic=containers-plan_vpc_basics#vpc-pgw). You cannot change the cloud service endpoints after you create the cluster.

Ingress secrets management
:   [{{site.data.keyword.secrets-manager_full_notm}}](/docs/openshift?topic=openshift-secrets-mgr) centrally manages Ingress subdomain certificates and other secrets in your cluster. You can choose to register a {{site.data.keyword.secrets-manager_short}} instance to your cluster during the cluster create process. You can also specify a secret group that you can use to control access to the secrets in your cluster. Both of these options can be configured or changed after you have created the cluster. 

Encryption
:    Enable data encryption with a key management service (KMS) to encrypt secrets and other sensitive information in your cluster. You can also [enable KMS](/docs/openshift?topic=openshift-encryption-setup) later. 


Cluster details
:   You can customize the unique cluster name and any [tags](/docs/account?topic=account-tag) that you want to use to organize and identify your {{site.data.keyword.cloud_notm}} resources, such as the `team` or `billing department`. 


Observability integrations
:    You can enable additional observability integrations that you want to include on your cluster. Some integrations are automatically enabled if you have an existing platform instance of that integration. In this case, you cannot disable the integration. If you want to use an integration and you have only an existing application instance of that integration, the integration is disabled by default and you must manually enable it.
:    - [Logging]{: tag-dark-teal}: You can use {{site.data.keyword.logs_full_notm}} to manage operating system logs, application logs, and platform logs. If you want to enable this integration later, see [{{site.data.keyword.logs_full_notm}}](/docs/cloud-logs?topic=cloud-logs-about-cl).
:    - [Monitoring]{: tag-magenta}: The monitoring service integration allows operational visibility into the performance and health of your applications, services, and platforms. If you disable this integration and want to enable it later, see [Monitoring cluster health](/docs/openshift?topic=openshift-health-monitor&interface=ui).The Security and Compliance Center Workload Protection integration finds and prioritizes software vulnerabilities, detects and responds to threats, and manages configurations, permissions, and compliance from source to run. For more information, see the Workload Protection [Getting Started](/docs/workload-protection?topic=workload-protection-getting-started) page.
    - Specify the **Configuration type** to use either new or existing instances of Monitoring and Workload Protection. If you use want to use existing instances of both Monitoring and Workload protection, the instances of each integration must be connected. In this case, specify either the Monitoring or Workload Protection instance you want to use; you cannot specify both instances, but both instances are used as long as they are connected. You can connect existing instances from the details page of either the [Monitoring](https://cloud.ibm.com/observability/monitoring){: external} or [Workload Protection](https://cloud.ibm.com/security-compliance){: external} instance. 

## Creating a classic cluster in the CLI
{: #clusters_cli_steps}
{: cli}

Create your Classic cluster by using the {{site.data.keyword.cloud_notm}} CLI.
{: shortdesc}

* Ensure that you complete the prerequisites to [prepare your account](/docs/openshift?topic=openshift-clusters) and decide on your cluster setup. Keep in mind that you need a cluster with a minimum of 2 worker nodes of the `4x16` flavor so that default {{site.data.keyword.redhat_openshift_notm}} components can deploy.
* [Install the {{site.data.keyword.cloud_notm}} CLI tools](/docs/openshift?topic=openshift-cli-install).

1. Log in to {{site.data.keyword.cloud_notm}} CLI. If you are logging in with a federated ID, use `ibmcloud login --sso`.

    ```sh
    ibmcloud login [--sso]
    ```
    {: pre}

1. If you have multiple {{site.data.keyword.cloud_notm}} accounts, select the account where you want to create your cluster.

1. To create clusters in a resource group other than default, target that resource group. A cluster can be created in only one resource group, and after the cluster is created, you can't change its resource group. You must have at least the [**Viewer** role](/docs/openshift?topic=openshift-iam-platform-access-roles) for the resource group to target it.

    ```sh
    ibmcloud target -g <resource_group_name>
    ```
    {: pre} 

1. Review the zones where you can create your cluster. In the output of the following command, zones have a **Location Type** of `dc`. To span your cluster across zones, you must create the cluster in a [multizone-capable zone](/docs/openshift?topic=openshift-regions-and-zones#zones-mz). Multizone-capable zones have a metro value in the **Multizone Metro** column. If you want to create a multizone cluster, you can use the {{site.data.keyword.cloud_notm}} console, or [add more zones](/docs/openshift?topic=openshift-add-workers-classic) to your cluster after the cluster is created.
    ```sh
    ibmcloud oc locations
    ```
    {: pre}

    When you select a zone that is located outside your country, keep in mind that you might require legal authorization before data can be physically stored in a foreign country.
    {: note}

1. Review the worker node flavors that are available in that zone. The flavor determines the amount of virtual CPU, memory, and disk space that is set up in each worker node and made available to your apps. Worker nodes in classic clusters can be created as virtual machines on shared or dedicated infrastructure, or as bare metal machines that are dedicated to you. After you create your cluster, you can add different flavors by [adding a worker pool](/docs/openshift?topic=openshift-add-workers-classic).

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
    ibmcloud oc cluster create classic --zone <zone> --flavor <flavor> --hardware <shared_or_dedicated> --public-vlan <public_VLAN_ID> --private-vlan <private_VLAN_ID> --workers <number> [--operating-system (REDHAT_8_64)] --name <cluster_name> --version <major.minor.patch>_openshift --public-service-endpoint [--private-service-endpoint] [--pod-subnet] [--service-subnet] [--disable-disk-encrypt] [--sm-group GROUP] [--sm-instance INSTANCE] 
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
    :   Specify the number of worker nodes to include in the cluster. The default value is 1.

    `--version <major.minor.patch>`
    :   The {{site.data.keyword.redhat_openshift_notm}} version for the cluster master node. This value is required. When the version is not specified, the cluster is created with the default supported Kubernetes version. If you don't specify a supported {{site.data.keyword.redhat_openshift_notm}} version, your cluster is created as a community Kubernetes cluster. To see available versions, run `ibmcloud oc versions`.

    `--public-service-endpoint`
    :   Enable the public cloud service endpoint so that your {{site.data.keyword.redhat_openshift_notm}} master can be accessed over the public network, for example to run `oc` commands from your CLI, and so that your {{site.data.keyword.redhat_openshift_notm}} master and the worker nodes can communicate over the public VLAN. You must enable the public cloud service endpoint, and can't later disable it.After you create the cluster, you can get the endpoint by running `ibmcloud oc cluster get --cluster <cluster_name_or_ID>`.

    `--private-service-endpoint`
    :   In [VRF-enabled](/docs/account?topic=account-vrf-service-endpoint&interface=ui) and [service endpoint-enabled accounts](/docs/account?topic=account-vrf-service-endpoint#service-endpoint): Enable the private cloud service endpoint so that your {{site.data.keyword.redhat_openshift_notm}} master and the worker nodes can communicate over the private VLAN. If you specify this option, you must also enable the public cloud service endpoint by using the `--public-service-endpoint` option. Note that you can't later change the cloud service endpoints.After you create the cluster, you can get the endpoint by running `ibmcloud oc cluster get --cluster <cluster_name_or_ID>`.

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
    
    `--entitlement ocp_entitled`
    :   Include this option only for a cluster that has a {{site.data.keyword.redhat_openshift_notm}} entitlement. When you specify the number of workers (`--workers`) and flavor (`--flavor`), make sure to specify only the number and size of worker nodes that you are entitled to use in [IBM Passport Advantage](https://www.ibm.com/software/passportadvantage/index.html){: external}. After your cluster is created, you are not charged the {{site.data.keyword.redhat_openshift_notm}} license fee for the entitled worker nodes in the `default` worker pool.
    Do not exceed your entitlement. Keep in mind that your OpenShift Container Platform entitlements can be used with other cloud providers or in other environments. To avoid billing issues later, make sure that you use only what you are entitled to use. For example, you might have an entitlement for the OCP licenses for two worker nodes of 4 CPU and 16 GB memory, and you create this worker pool with two worker nodes of 4 CPU and 16 GB memory. You used your entire entitlement, and you can't use the same entitlement for other worker pools, cloud providers, or environments.
    {: important}

    `--sm-group GROUP`
    :    The secret group ID of the {{site.data.keyword.secrets-manager_short}} instance where your secrets are persisted. To get a secret group ID, see the [{{site.data.keyword.secrets-manager_short}} CLI reference](/docs/secrets-manager?topic=secrets-manager-secrets-manager-cli#secrets-manager-cli-secret-groups-command).

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
    mycluster    blrs3b1d0p0p2f7haq0g       normal   20170201162433   3          dal10     4.18.19_1544_openshift      Default             classic
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
    kube-blrs3b1d0p0p2f7haq0g-mycluster-default-000001f7   169.xx.xxx.xxx  10.xxx.xx.xxx   u3c.2x4.encrypted   normal   Ready    dal10   1.32.7_1526
    ```
    {: screen}

    Every worker node is assigned a unique worker node ID and domain name that must not be changed manually after the cluster is created. If you change the ID or domain name, the {{site.data.keyword.redhat_openshift_notm}} master cannot manage your cluster.
    {: important}

1. **Optional**: If you created your cluster in a [multizone region](/docs/openshift?topic=openshift-regions-and-zones#zones-mz), you can [spread the default worker pool across zones](/docs/openshift?topic=openshift-add-workers-classic) to increase the cluster's availability.

1. After your cluster is created, you can [begin working with your cluster by configuring your CLI session](/docs/openshift?topic=openshift-access_cluster).

Your cluster is ready for your workloads! You might also want to [add a tag to your cluster](/docs/openshift?topic=openshift-worker-tag-label), such as the team or billing department that uses the cluster, to help manage {{site.data.keyword.cloud_notm}} resources.




## Example commands to create classic clusters
{: #cluster_create_classic}
{: cli}

Example command to create a Classic cluster on shared virtual machine.

```sh
ibmcloud oc cluster create classic --name my_cluster --version 4.18_openshift --zone dal10 --flavor b3c.4x16 --hardware shared --workers 3
```
{: pre}


Example command to create a Classic cluster on bare metal.

```sh
ibmcloud oc cluster create classic --name my_cluster --version 4.18_openshift --zone dal10 --flavor mb2c.4x32 --hardware dedicated --workers 3 --public-vlan <public_VLAN_ID> --private-vlan <private_VLAN_ID>
```
{: pre}

Example command to create a Classic cluster with an IBM Cloud Pak entitlement for a default worker pool of 3 worker nodes with 4 cores and 16 memory each.

```sh
ibmcloud oc cluster create classic --name cloud_pak_cluster --version 4.18_openshift --zone dal10 --flavor b3c.4x16 --hardware dedicated --workers 3 --entitlement ENTITLEMENT --public-vlan PUBLIC-VLAN-ID --private-vlan PRIVATE-VLAN-ID [--operating-system (REDHAT_8_64)]
```
{: pre}


Example command to create a Classic cluster with RHEL 9 worker nodes.

```sh
ibmcloud oc cluster create classic --name my_cluster --zone dal10 --flavor b3c.4x16 --version 4.9.28_openshift --operating-system RHEL_9_64
```
{: pre}




For a classic multizone cluster, after you created the cluster in a [multizone metro](/docs/openshift?topic=openshift-regions-and-zones#zones-mz), [add zones](/docs/openshift?topic=openshift-add-workers-classic). Example command to add a zone to a Classic cluster.
```sh
ibmcloud oc zone add classic --zone <zone> --cluster <cluster_name_or_ID> --worker-pool <pool_name> --private-vlan <private_VLAN_ID> --public-vlan <public_VLAN_ID>
```
{: pre}


## Creating a single-zone classic cluster with Terraform
{: #cluster_classic_tf}
{: terraform}

Terraform on {{site.data.keyword.cloud_notm}} enables predictable and consistent provisioning of {{site.data.keyword.cloud_notm}} platform infrastructure and resources, including classic clusters. To create a classic cluster with Terraform, you first create a Terraform configuration file that declares the type of cluster resource you want to create. Then, you apply the Terraform configuration file. For more information on Terraform, see [About Terraform on {{site.data.keyword.cloud_notm}}](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-about).

**Before you begin:**
* [Install the Terraform CLI and the {{site.data.keyword.cloud_notm}} Provider plug-in](/docs/ibm-cloud-provider-for-terraform?topic=ibm-cloud-provider-for-terraform-setup_cli#tf_installation).
* Make sure you have an {{site.data.keyword.cloud_notm}} [API key](/docs/account?topic=account-userapikey&interface=ui#create_user_key). 



1. Create a Terraform provider file. Save the file in your Terraform directory. For more information, see the [Terraform IBM Cloud Provider documentation](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs){: external}. 

    Example Terraform provider file. 

    ```sh
    terraform {
    required_providers {
        ibm = {
        source = "IBM-Cloud/ibm"
        version = "1.53.0"
        }
    }
    }

    provider "ibm" {
    region = "us-south"
    ibmcloud_api_key = "<api-key>"
    }
    ```
    {: pre}

2. Create a Terraform configuration file for a classic cluster. Save the file in your Terraform directory. The following example configuration creates a classic cluster with three worker nodes in one zone. For more information and cluster configuration options, see the [Terraform `ibm_container_cluster`](https://registry.terraform.io/providers/IBM-Cloud/ibm/latest/docs){: external} documentation. 

    Example Terraform configuration file. 
    ```sh
    resource "ibm_container_cluster" "testacc_cluster" {
    name            = "test-classic"
    datacenter      = "dal10"
    machine_type    = "b3c.4x16"
    hardware        = "shared"
    public_vlan_id  = "<vlan_id>"
    private_vlan_id = "<vlan_id"
    subnet_id       = ["<subnet_id>"]

    default_pool_size = 3
    }
    ```
    {: pre}

    `name`
    :   The name of the cluster.

    `datacenter`
    :   The zone to create the cluster in. To see available zones, run `ibmcloud oc zones --provider classic`.

    `machine_type`
    :   The worker node flavor. The flavor determines the amount of memory, CPU, and disk space that is available to your worker nodes. For a list of available worker node flavors, run `ibmcloud oc flavors --zone <zone> --provider classic`, or see [Classic flavors](/docs/openshift?topic=openshift-classic-flavors).

    `hardware`
    :   The level of hardware isolation for your worker nodes. Use `dedicated` to have available physical resources dedicated to you only, or `shared` to allow physical resources to be shared with other IBM customers. This option is available for virtual machine worker nodes flavors only. 

    `public_vlan_id` and `private_vlan_id`
    :   Optional. The ID of the public or private VLAN that you want to use for your worker nodes. To find available VLANs and subnets, run `ibmcloud oc vlans --zone <zone>`.

    `subnet_id`
    :   Optional. The ID of an existing subnet that you want to use for your worker nodes. To find existing subnets, run `ibmcloud oc subnets --provider classic --zone <zone>`.

    `default_pool_size`
    :   The number of worker nodes that you want to add to the default worker pool. 

3. In the CLI, navigate to your Terraform directory.
    ```sh
    cd <terraform_directory>
    ```
    {: pre}

4. Run the commands to initialize and plan your Terraform actions. Review the plan output to make sure the correct actions are performed. 

    ```sh
    terraform init
    ```
    {: pre}

    ```sh
    terraform plan
    ```
    {: pre}

5. Apply the Terraform files to create the cluster. Then, navigate to the IBM Cloud console to check that the cluster is provisioning.
    ```sh
    terraform apply
    ```
    {: pre}
    
    
## Next steps for Classic clusters
{: #cluster-create-classic-next-steps}

* Isolate networking workloads to edge worker nodes [in classic clusters without a gateway](/docs/openshift?topic=openshift-edge).
* Expose your apps with [public networking services](/docs/openshift?topic=openshift-cs_network_planning#openshift_routers) or [private networking services](/docs/openshift?topic=openshift-cs_network_planning#private_access). If you have multiple public clusters with exposed apps, consider connecting them with a [global load balancer](/docs/containers?topic=containers-strategy#plan_locations) for high availability. 
* Connect your cluster with services in private networks outside of your {{site.data.keyword.cloud_notm}} account by setting up [{{site.data.keyword.dl_full_notm}}](/docs/dl?topic=dl-get-started-with-ibm-cloud-dl) or the [strongSwan IPSec VPN service](/docs/openshift?topic=openshift-vpn).
* Create Calico host network policies to isolate your cluster on the [public network](/docs/openshift?topic=openshift-network_policies#isolate_workers_public) and on the [private network](/docs/openshift?topic=openshift-network_policies#isolate_workers).
* If you use a gateway appliance, such as a Virtual Router Appliance (VRA), [open up the required ports and IP addresses](/docs/openshift?topic=openshift-firewall#firewall_inbound) in the public firewall to permit inbound traffic to networking services. If you also have a firewall on the private network, [allow communication between worker nodes and let your cluster access infrastructure resources over the private network](/docs/openshift?topic=openshift-firewall#firewall_private).
