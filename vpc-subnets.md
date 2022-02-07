---

copyright: 
  years: 2014, 2022
lastupdated: "2022-02-07"

keywords: openshift, ips, vlans, networking, public gateway

subcollection: openshift


---


{{site.data.keyword.attribute-definition-list}}


# Configuring VPC subnets
{: #vpc-subnets}

Change the pool of available portable public or private IP addresses by adding subnets to your {{site.data.keyword.openshiftlong}} VPC cluster.
{: shortdesc}

![VPC infrastructure provider icon.](images/icon-vpc-2.svg) The content on this page is specific to VPC clusters. For information about classic clusters, see [Configuring subnets and IP addresses for classic clusters](/docs/containers?topic=containers-subnets).
{: note}

## Overview of VPC networking in {{site.data.keyword.openshiftlong_notm}}
{: #vpc_basics}

Understand the basic concepts of VPC networking in {{site.data.keyword.openshiftlong_notm}} clusters.
{: shortdesc}

### Subnets
{: #vpc_basics_subnets}

Before you create a VPC cluster for the first time, you must [create a VPC subnet](https://cloud.ibm.com/vpc/provision/network){: external} in each zone where you want to deploy worker nodes. A VPC subnet is a specified private IP address range (CIDR block) and configures a group of worker nodes and pods as if they are attached to the same physical wire.
{: shortdesc}

When you create a cluster, you can specify only one existing VPC subnet for each zone. Each worker node that you add in a cluster is deployed with a private IP address from the VPC subnet in that zone. After the worker node is provisioned, the worker node IP address persists after a `reboot` operation, but the worker node IP address changes after `replace` and `update` operations.

Do not delete the subnets that you attach to your cluster during cluster creation or when you add worker nodes in a zone. If you delete a VPC subnet that your cluster used, any load balancers that use IP addresses from the subnet might experience issues, and you might be unable to create new load balancers.
{: important}

**How many IP addresses do I need for my VPC subnet?**

When you [create your VPC subnet](https://cloud.ibm.com/vpc/provision/network){: external}, make sure to create a subnet with enough IP addresses for your cluster, such as 256. You can't change the number of IP addresses that a VPC subnet has later.

Keep in mind the following IP address reservations.
- 5 IP addresses are [reserved by VPC](/docs/vpc?topic=vpc-about-networking-for-vpc#addresses-reserved-by-the-system) from each subnet by default.
- {{site.data.keyword.openshiftshort}} version 4.6 or later: 1 IP address from one subnet in each zone where your cluster has worker nodes is required for the [virtual private endpoints (VPE) gateway](#vpc_basics_vpe).
- 1 IP address is required per worker node in your cluster.
- 1 IP address is required each time that you update or replace a worker node. These IP addresses are eventually reclaimed and available for reuse.
- 2 IP addresses are used each time that you create a public or private load balancer. If you have a multizone cluster, these 2 IP addresses are spread across zones, so the subnet might not have an IP address reserved.
- Other networking resources that you set up for the cluster, such as a VPNaaS or LBaaS autoscaling, might require additional IP addresses or have other [service limitations](/docs/vpc?topic=vpc-limitations). For example, LBaaS autoscaling might scale up to 16 IP addresses per load balancer.

**What IP ranges can I use for my VPC subnets?**


The default IP address range for VPC subnets is 10.0.0.0 – 10.255.255.255. For a list of IP address ranges per VPC zone, see the [VPC default address prefixes](/docs/vpc?topic=vpc-configuring-address-prefixes). {: #vpc-ip-range}

If you need to create your cluster by using custom-range subnets, see the guidance for [custom address prefixes](/docs/vpc?topic=vpc-configuring-address-prefixes). However, if you use custom-range subnets for your worker nodes, you must ensure that the IP range for the worker node subnets don't overlap with your cluster's pod subnet.
* If you specified your own pod subnet in the `--pod-subnet` flag during cluster creation, your pods are assigned IP addresses from this range.
* If you did not specify a custom pod subnet during cluster creation, your cluster uses the default pod subnet. In the first cluster that you create in a VPC, the default pod subnet is `172.17.0.0/18`. In the second cluster that you create in that VPC, the default pod subnet is `172.17.64.0/18`. In each subsequent cluster, the pod subnet range is the next available, non-overlapping `/18` subnet.

**How do I create subnets for classic infrastructure access?**

If you enable classic access when you create your VPC, [classic access default address prefixes](/docs/vpc?topic=vpc-setting-up-access-to-classic-infrastructure#classic-access-default-address-prefixes) automatically determine the IP ranges of any subnets that you create. However, the default IP ranges for classic access VPC subnets conflict with the subnets for the {{site.data.keyword.openshiftlong_notm}} control plane. Instead, you must [create the VPC without the automatic default address prefixes, and then create your own address prefixes and subnets within those ranges for you cluster](#classic_access_subnets).

**Can I specify subnets for pods and services in my cluster?**

If you plan to connect your cluster to on-premises networks through {{site.data.keyword.dl_full_notm}} or a VPN service, you can avoid subnet conflicts by specifying a custom subnet CIDR that provides the private IP addresses for your pods, and a custom subnet CIDR to provide the private IP addresses for services.

To specify custom pod and service subnets during cluster creation, use the `--pod-subnet` and `--service-subnet` flags in the `ibmcloud oc cluster create` CLI command.

To see the pod and service subnets that your cluster uses, look for the `Pod Subnet` and `Service Subnet` fields in the output of `ibmcloud oc cluster get`.

#### Pods
{: #vpc_basics_subnets_pods}

Default range
: In the first cluster that you create in a VPC, the default pod subnet is `172.17.0.0/18`. In the second cluster that you create in that VPC, the default pod subnet is `172.17.64.0/18`. In each subsequent cluster, the pod subnet range is the next available, non-overlapping `/18` subnet.

Size requirements
:   When you specify a custom subnet, consider the size of the cluster that you plan to create and the number of worker nodes that you might add in the future. The subnet must have a CIDR of at least `/23`, which provides enough pod IPs for a maximum of four worker nodes in a cluster. For larger clusters, use `/22` to have enough pod IP addresses for eight worker nodes, `/21` to have enough pod IP addresses for 16 worker nodes, and so on.

Range requirements
:   The pod and service subnets can't overlap each other, and the pod subnet can't overlap the VPC subnets for your worker nodes. The subnet that you choose must be within one of the following ranges.
    - `172.17.0.0 - 172.17.255.255`
    - `172.21.0.0 - 172.31.255.255`
    - `192.168.0.0 - 192.168.254.255`
    - `198.18.0.0 - 198.19.255.255`

#### Services
{: #vpc_basics_subnets_services}

Default range
:   All services that are deployed to the cluster are assigned a private IP address in the `172.21.0.0/16` range by default.

Size requirements
:   When you specify a custom subnet, the subnet must be specified in CIDR format with a size of at least `/24`, which allows a maximum of 255 services in the cluster, or larger.

Range requirements
:   The pod and service subnets can't overlap each other. The subnet that you choose must be within one of the following ranges.
    - `172.17.0.0 - 172.17.255.255`
    - `172.21.0.0 - 172.31.255.255`
    - `192.168.0.0 - 192.168.254.255`
    - `198.18.0.0 - 198.19.255.255`

### Public gateways
{: #vpc_basics_pgw}

A public gateway enables a subnet and all worker nodes that are attached to the subnet to establish outbound connections to the internet. If both the public and private cloud service endpoints are enabled for your cluster, you must enable a [public gateway](/docs/vpc?topic=vpc-about-networking-for-vpc#public-gateway-for-external-connectivity) on the VPC subnets that worker nodes are deployed to to access default {{site.data.keyword.openshiftshort}} components without being connected to your VPC's private network.
{: shortdesc}

When you create a VPC cluster and enable both the public and private cloud service endpoints during cluster creation, the public cloud service endpoint is used by default for access to components such as the {{site.data.keyword.openshiftshort}} web console for your cluster. In order for console pods to establish a secure, public connection over the internet through the public service endpoint, you must enable a public gateway on each VPC subnet that your worker nodes are deployed to.

When you create a VPC cluster and enable only the private cloud service endpoint during cluster creation, the private cloud service endpoint is used by default to access {{site.data.keyword.openshiftshort}} components such as the {{site.data.keyword.openshiftshort}} web console or OperatorHub. You must be connected to the private VPC network, such as through a VPN connection, to access these components or run `kubectl` commands on your cluster. Also, if an {{site.data.keyword.cloud_notm}} service does not support private cloud service endpoints, your worker nodes must be connected to a subnet that has a public gateway attached to it. The pods on those worker nodes can securely communicate with the services over the public network through the subnet's public gateway. Note that a public gateway is not required on your subnets to allow inbound network traffic from the internet to `LoadBalancer` services or ALBs.

Within one VPC, you can create only one public gateway per zone, but that public gateway can be attached to multiple subnets within the zone. For more information about public gateways, see the [Networking for VPC documentation](/docs/vpc?topic=vpc-about-networking-for-vpc#public-gateway-for-external-connectivity).

### Virtual private endpoints (VPE)
{: #vpc_basics_vpe}

In clusters that run {{site.data.keyword.openshiftshort}} version 4.6 or later, worker nodes can communicate with the Kubernetes master through the cluster's [virtual private endpoint (VPE)](/docs/vpc?topic=vpc-about-vpe).
{: shortdesc}

A VPE is a virtual IP address that is bound to an endpoint gateway. One VPE gateway resource is created per cluster in your VPC. One IP address from one subnet in each zone where your cluster has worker nodes is automatically used for the VPE gateway, and the worker nodes in this zone use this IP address to communicate with the Kubernetes master. To view the VPE gateway details for your cluster, open the [Virtual private endpoint gateways for VPC dashboard](https://cloud.ibm.com/vpc-ext/network/endpointGateways){: external} and look for the VPE gateway in the format `iks-<cluster_ID>`.

Note that your worker nodes automatically use the VPE that is created by default in your VPC. However, if you enabled the [public cloud service endpoint for your cluster](/docs/openshift?topic=openshift-plan_clusters#vpc-workeruser-master), worker-to-master traffic is established half over the public endpoint and half over the VPE for protection from potential outages of the public or private network.

Do not delete any IP addresses on your subnets that are used for VPEs.
{: important}

### Network segmentation
{: #vpc_basics_segmentation}

Network segmentation describes the approach to divide a network into multiple sub-networks. Apps that run in one sub-network can't see or access apps in another sub-network. For more information about network segmentation options for VPC subnets, see [this cluster security topic](/docs/openshift?topic=openshift-security#network_segmentation_vpc).
{: shortdesc}

Subnets provide a channel for connectivity among the worker nodes within the cluster. Additionally, any system that is connected to any of the private subnets in the same VPC can communicate with workers. For example, all subnets in one VPC can communicate through private layer 3 routing with a built-in VPC router.

If you have multiple clusters that must communicate with each other, you can create the clusters in the same VPC. However, if your clusters don't need to communicate, you can achieve better network segmentation by creating the clusters in separate VPCs. You can also create [access control lists (ACLs)](/docs/containers?topic=containers-vpc-network-policy) for your VPC subnets to mediate traffic on the private network. ACLs consist of inbound and outbound rules that define which ingress and egress is permitted for each VPC subnet.

### VPC networking limitations
{: #vpc_basics_limitations}

When you create VPC subnets for your clusters, keep in mind the following features and limitations.
{: shortdesc}

- The default CIDR size of each VPC subnet is `/24`, which can support up to 253 worker nodes. If you plan to deploy more than 250 worker nodes per zone in one cluster, consider creating a subnet of a larger size.
- After you create a VPC subnet, you can't resize it or change its IP range.
- Multiple clusters in the same VPC can share VPC subnets. However, custom pod and service subnets can't be shared between multiple clusters.
- VPC subnets are bound to a single zone and can't span multiple zones or regions.
- After you create a subnet, you can't move it to a different zone, region, or VPC.
- If you have worker nodes that are attached to an existing subnet in a zone, you can't change the subnet for that zone in the cluster.
- The `172.16.0.0/16`, `172.18.0.0/16`, `172.19.0.0/16`, and `172.20.0.0/16` ranges are prohibited.
- Within one VPC, you can create only one public gateway per zone, but that public gateway can be attached to multiple subnets within the zone.
- The [classic access default address prefixes](/docs/vpc?topic=vpc-setting-up-access-to-classic-infrastructure#classic-access-default-address-prefixes) conflict with the subnets for the {{site.data.keyword.openshiftlong_notm}} control plane. You must [create the VPC without the automatic default address prefixes, and then create your own address prefixes and subnets within those ranges for you cluster](#classic_access_subnets).




## Creating a VPC subnet and attaching a public gateway
{: #create_vpc_subnet}

Create a VPC subnet for your cluster and optionally attach a public gateway to the subnet.
{: shortdesc}

### Creating a VPC subnet in the console
{: #create_vpc_subnet_ui}

Use the {{site.data.keyword.cloud_notm}} console to create a VPC subnet for your cluster and optionally attach a public gateway to the subnet.
{: shortdesc}

1. From the [VPC subnet dashboard](https://cloud.ibm.com/vpc/network/subnets), click **Create**.
2. Enter a name for your subnet and select the name of the VPC that you created.
3. Select the location and zone where you want to create the subnet.
4. Specify the number of IP addresses to create.
    - VPC subnets provide IP addresses for your worker nodes and load balancer services in the cluster, so [create a VPC subnet with enough IP addresses](/docs/openshift?topic=openshift-vpc-subnets#vpc_basics_subnets), such as 256. You can't change the number of IPs that a VPC subnet has later.
    - If you enter a specific IP range and running Red Hat OpenShift 4.7 or earlier., don't use the following reserved ranges: `172.16.0.0/16`, `172.18.0.0/16`, `172.19.0.0/16`, and `172.20.0.0/16`.
5. To run default {{site.data.keyword.openshiftshort}} components such as the web console or OperatorHub, and to allow your cluster to access public endpoints such as a public URL of another app or an {{site.data.keyword.cloud_notm}} service that supports public cloud service endpoints only, you must attach a public gateway to your subnet.
6. Click **Create subnet**.
7. Use the subnet to [create a cluster](/docs/openshift?topic=openshift-clusters#clusters_vpcg2_ui), [create a new worker pool](/docs/openshift?topic=openshift-add_workers#vpc_add_pool), or [add the subnet to an existing worker pool](/docs/openshift?topic=openshift-add_workers#vpc_add_zone).>
    Do not delete the subnets that you attach to your cluster during cluster creation or when you add worker nodes in a zone. If you delete a VPC subnet that your cluster used, any load balancers that use IP addresses from the subnet might experience issues, and you might be unable to create new load balancers.
    {: important}

### Creating a VPC subnet in the CLI
{: #create_vpc_subnet_cli}

Use the {{site.data.keyword.cloud_notm}} CLI to create a VPC subnet for your cluster and optionally attach a public gateway to the subnet.
{: shortdesc}

Before you begin

1. In your command line, log in to your {{site.data.keyword.cloud_notm}} account and target the {{site.data.keyword.cloud_notm}} region and resource group where you want to create your VPC cluster. For supported regions, see [Creating a VPC in a different region](/docs/vpc?topic=vpc-creating-a-vpc-in-a-different-region). The cluster's resource group can differ from the VPC resource group. Enter your {{site.data.keyword.cloud_notm}} credentials when prompted. If you have a federated ID, use the `--sso` flag to log in.
    ```sh
    ibmcloud login -r <region> [-g <resource_group>] [--sso]
    ```
    {: pre}

2. [Create a VPC](/docs/vpc?topic=vpc-creating-a-vpc-using-cli#create-a-vpc-cli) in the same region where you want to create the cluster.

To create a VPC subnet, follow these steps.

1. Get the ID of the VPC where you want to create the subnet.
    ```sh
    ibmcloud oc vpcs
    ```
    {: pre}

2. Create the subnet. For more information about the options in this command, see the [CLI reference](/docs/vpc?topic=vpc-creating-a-vpc-using-cli#create-a-subnet-cli).
    ```sh
    ibmcloud is subnet-create <subnet_name> <vpc_id> --zone <vpc_zone> --ipv4-address-count <number_of_ip_address>
    ```
    {: pre}

    - VPC subnets provide IP addresses for your worker nodes and load balancer services in the cluster, so [create a VPC subnet with enough IP addresses](/docs/openshift?topic=openshift-vpc-subnets#vpc_basics_subnets), such as 256. You can't change the number of IPs that a VPC subnet has later.
    - If you are running Red Hat OpenShift 4.7 or earlier, don't use the following reserved ranges: `172.16.0.0/16`, `172.18.0.0/16`, `172.19.0.0/16`, and `172.20.0.0/16`.

3. Check whether you have a public gateway in the zones where you want to create a cluster. Within one VPC, you can create only one public gateway per zone, but that public gateway can be attached to multiple subnets within the zone.
    ```sh
    ibmcloud is public-gateways
    ```
    {: pre}

    Example output

    ```sh
    ID                                     Name                                       VPC                          Zone         Floating IP                  Created                     Status      Resource group
    26426426-6065-4716-a90b-ac7ed7917c63   test-pgw                                   testvpc(36c8f522-.)          us-south-1   169.xx.xxx.xxx(26466378-.)   2019-09-20T16:27:32-05:00   available   -
    2ba2ba2b-fffa-4b0c-bdca-7970f09f9b8a   pgw-73b62bc0-b53a-11e9-9838-f3f4efa02374   team3(ff537d43-.)            us-south-2   169.xx.xxx.xxx(2ba9a280-.)   2019-08-02T10:30:29-05:00   available   -
    ```
    {: screen}

    - If you already have a public gateway in each zone, note the **ID**s of the public gateways.
    - If you don't have a public gateway in each zone, create a public gateway. Consider naming the public gateway in the format `<cluster>-<zone>-gateway`. In the output, note the public gateway's **ID**.
    ```sh
    ibmcloud is public-gateway-create <gateway_name> <VPC_ID> <zone>
    ```
    {: pre}

    Example output

    ```sh
    ID               26466378-6065-4716-a90b-ac7ed7917c63
    Name             mycluster-us-south-1-gateway
    Floating IP      169.xx.xx.xxx(26466378-6065-4716-a90b-ac7ed7917c63)
    Status           pending
    Created          2019-09-20T16:27:32-05:00
    Zone             us-south-1
    VPC              myvpc(36c8f522-4f0d-400c-8226-299f0b8198cf)
    Resource group   -
    ```
    {: screen}

4. Using the IDs of the public gateway and the subnet, attach the public gateway to the subnet.
    ```sh
    ibmcloud is subnet-update <subnet_ID> --public-gateway-id <gateway_ID>
    ```
    {: pre}

    Example output

    ```sh
    ID                  91e946b4-7094-46d0-9223-5c2dea2e5023
    Name                mysubnet1
    IPv4 CIDR           10.240.xx.xx/24
    Address available   250
    Address total       256
    ACL                 allow-all-network-acl-36c8f522-4f0d-400c-8226-299f0b8198cf(585bc142-5392-45d4-afdd-d9b59ef2d906)
    Gateway             mycluster-us-south-1-gateway(26466378-6065-4716-a90b-ac7ed7917c63)
    Created             2019-08-21T09:43:11-05:00
    Status              available
    Zone                us-south-1
    VPC                 myvpc(36c8f522-4f0d-400c-8226-299f0b8198cf)
    ```
    {: screen}


5. Use the subnet to [create a cluster](/docs/openshift?topic=openshift-clusters#cluster_vpcg2_cli), [create a new worker pool](/docs/openshift?topic=openshift-add_workers#vpc_add_pool), or [add the subnet to an existing worker pool](/docs/openshift?topic=openshift-add_workers#vpc_add_zone).
    Do not delete the subnets that you attach to your cluster during cluster creation or when you add worker nodes in a zone. If you delete a VPC subnet that your cluster used, any load balancers that use IP addresses from the subnet might experience issues, and you might be unable to create new load balancers.
    {: important}


## Creating VPC subnets for classic access
{: #classic_access_subnets}

If you enable classic access when you create your VPC, [classic access default address prefixes](/docs/vpc?topic=vpc-setting-up-access-to-classic-infrastructure#classic-access-default-address-prefixes) automatically determine the IP ranges of any subnets that you create. However, the default IP ranges for classic access VPC subnets conflict with the subnets for the {{site.data.keyword.openshiftlong_notm}} control plane. Instead, you must create the VPC without the automatic default address prefixes, and create your own address prefixes. Then, whenever you create subnets for your cluster, you create the subnets within the address prefix ranges that you created.
{: shortdesc}

### Creating VPC subnets for classic access in the console
{: #ca_subnet_ui}

1. Create a classic access VPC without default address prefixes.
    1. From the [Virtual Private Clouds dashboard](https://cloud.ibm.com/vpc/provision/vpc), click **Create**.
    2. Enter details for the name, resource group, and any tags.
    3. Select the checkbox for **Enable access to classic resources**, and clear the checkbox for **Create a default prefix for each zone**.
    4. Select the region for the VPC.
    5. Click **Create virtual private cloud**.
2. Create address prefixes in each zone.
    1. Click the name of your VPC to view its details.
    2. Click the **Address prefixes** tab and click **Create**.
    3. For each zone in which you plan to create subnets, create one or more address prefixes. The address prefixes must be within one of the following ranges: `10.0.0.0 - 10.255.255.255`, `172.17.0.0 - 172.17.255.255`, `172.21.0.0 - 172.31.255.255`, `192.168.0.0 - 192.168.254.255`.
3. Create subnets that use your address prefixes.
    1. From the [VPC subnet dashboard](https://cloud.ibm.com/vpc/network/subnets), click **Create**.
    2. Enter a name for your subnet and select the name of your classic access VPC.
    3. Select the location and zone where you want to create the subnet.
    4. Select the address prefix that you created for this zone.
    5. Specify the number of IP addresses to create. VPC subnets provide IP addresses for your worker nodes and load balancer services in the cluster, so [create a VPC subnet with enough IP addresses](/docs/openshift?topic=openshift-vpc-subnets#vpc_basics_subnets), such as 256. You can't change the number of IPs that a VPC subnet has later.
    6. To run default {{site.data.keyword.openshiftshort}} components such as the web console or OperatorHub, and to allow your cluster to access public endpoints such as a public URL of another app or an {{site.data.keyword.cloud_notm}} service that supports public cloud service endpoints only, you must attach a public gateway to your subnet.
    7. Click **Create subnet**.
4. Use the subnets to [create a cluster](/docs/openshift?topic=openshift-clusters#clusters_vpcg2_ui).
     Do not delete the subnets that you attach to your cluster during cluster creation or when you add worker nodes in a zone. If you delete a VPC subnet that your cluster used, any load balancers that use IP addresses from the subnet might experience issues, and you might be unable to create new load balancers.
     {: important}

### Creating VPC subnets for classic access from the CLI
{: #ca_subnet_cli}

1. In your command line, log in to your {{site.data.keyword.cloud_notm}} account and target the {{site.data.keyword.cloud_notm}} region and resource group where you want to create your VPC cluster. For supported regions, see [Creating a VPC in a different region](/docs/vpc?topic=vpc-creating-a-vpc-in-a-different-region). The cluster's resource group can differ from the VPC resource group. Enter your {{site.data.keyword.cloud_notm}} credentials when prompted. If you have a federated ID, use the `--sso` flag to log in.
    ```sh
    ibmcloud login -r <region> [-g <resource_group>] [--sso]
    ```
    {: pre}

2. Create a classic access VPC without default address prefixes. In the output, copy the VPC ID.
    ```sh
    ibmcloud is vpc-create <name> --classic-access --address-prefix-management manual
    ```
    {: pre}

3. For each zone in which you plan to create subnets, create one or more address prefixes. The address prefixes must be within one of the following ranges: `10.0.0.0 - 10.255.255.255`, `172.17.0.0 - 172.17.255.255`, `172.21.0.0 - 172.31.255.255`, `192.168.0.0 - 192.168.254.255`.
    ```sh
    ibmcloud is vpc-address-prefix-create <prefix_name> <vpc_id> <zone> <prefix_range>
    ```
    {: pre}

4. Create subnets in each zone that use your address prefixes. For more information about the options in this command, see the [CLI reference](/docs/vpc?topic=vpc-creating-a-vpc-using-cli#create-a-subnet-cli). VPC subnets provide IP addresses for your worker nodes and load balancer services in the cluster, so [create a VPC subnet with enough IP addresses](/docs/openshift?topic=openshift-vpc-subnets#vpc_basics_subnets), such as 256. You can't change the number of IPs that a VPC subnet has later.
    ```sh
    ibmcloud is subnet-create <subnet_name> <vpc_id> --zone <vpc_zone> --ipv4-address-count <number_of_ip_address> --ipv4-cidr-block <prefix_range>
    ```
    {: pre}

5. To run default {{site.data.keyword.openshiftshort}} components such as the web console or OperatorHub, and to allow your cluster to access public endpoints such as a public URL of another app or an {{site.data.keyword.cloud_notm}} service that supports public cloud service endpoints only, you must attach a public gateway to your subnet.
    1. Create a public gateway in each zone. Consider naming the public gateway in the format `<cluster>-<zone>-gateway`. In the output, note the public gateway's **ID**.
        ```sh
        ibmcloud is public-gateway-create <gateway_name> <VPC_ID> <zone>
        ```
        {: pre}

        Example output
        ```sh
        ID               26466378-6065-4716-a90b-ac7ed7917c63
        Name             mycluster-us-south-1-gateway
        Floating IP      169.xx.xx.xxx(26466378-6065-4716-a90b-ac7ed7917c63)
        Status           pending
        Created          2019-09-20T16:27:32-05:00
        Zone             us-south-1
        VPC              myvpc(36c8f522-4f0d-400c-8226-299f0b8198cf)
        Resource group   -
        ```
        {: screen}

    2. By using the IDs of the public gateway and the subnet, attach the public gateway to the subnet.
        ```sh
        ibmcloud is subnet-update <subnet_ID> --public-gateway-id <gateway_ID>
        ```
        {: pre}

        Example output
        ```sh
        ID                  91e946b4-7094-46d0-9223-5c2dea2e5023
        Name                mysubnet1
        IPv4 CIDR           10.240.xx.xx/24
        Address available   250
        Address total       256
        ACL                 allow-all-network-acl-36c8f522-4f0d-400c-8226-299f0b8198cf(585bc142-5392-45d4-afdd-d9b59ef2d906)
        Gateway             mycluster-us-south-1-gateway(26466378-6065-4716-a90b-ac7ed7917c63)
        Created             2019-08-21T09:43:11-05:00
        Status              available
        Zone                us-south-1
        VPC                 myvpc(36c8f522-4f0d-400c-8226-299f0b8198cf)
        ```
        {: screen}

6. Use the subnets to [create a cluster](/docs/openshift?topic=openshift-clusters#cluster_vpcg2_cli).
    Do not delete the subnets that you attach to your cluster during cluster creation or when you add worker nodes in a zone. If you delete a VPC subnet that your cluster used, any load balancers that use IP addresses from the subnet might experience issues, and you might be unable to create new load balancers.
    {: important}
    
 

