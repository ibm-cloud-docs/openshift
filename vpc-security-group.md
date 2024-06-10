---

copyright: 
  years: 2014, 2024
lastupdated: "2024-06-10"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, kubernetes, firewall, acl, acls, access control list, rules, security group

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}





# Understanding VPC security groups in version 4.14 and earlier
{: #vpc-security-group}
{: help}
{: support}

[Virtual Private Cloud]{: tag-vpc}
[4.14 and earlier]{: tag-red}

VPC clusters use various security groups to protect cluster components. These security groups are automatically created and attached to cluster workers, load balancers, and cluster-related VPE gateways. You can modify or replace these security groups to meet your specific requirements, however, any modifications must be made according to these guidelines to avoid network connectivity disruptions.
{: shortdesc}

Default behavior
:   Virtual Private Cloud security groups filter traffic at the hypervisor level. Security group rules are not applied in a particular order. However, requests to your worker nodes are only permitted if the request matches one of the rules that you specify. When you allow traffic in one direction by creating an inbound or outbound rule, responses are also permitted in the opposite direction. Security groups are additive, meaning that if your worker nodes are attached to more than one security group, all rules included in the security groups are applied to the worker nodes. Newer cluster versions might have more rules in the `kube-clusterID` security group than older cluster versions. Security group rules are added to improve the security of the service and do not break functionality.

Limitations
:   Because the worker nodes of your VPC cluster exist in a service account and aren't listed in the VPC infrastructure dashboard, you can't create a security group and apply it to your worker node instances. You can only modify the existing security group.


If you modify the default VPC security groups, you must, at minimum, include the required [inbound](#min-outbound-rules-sg-workers) and [outbound](#min-inbound-rules-sg-workers) rules so that your cluster works properly.  
{: important}

## Virtual private endpoint (VPE) gateways
{: #managed-vpe-gateways}

When the first VPC cluster at {{site.data.keyword.openshiftlong_notm}} 4.14+ is created in a given VPC, or a cluster in that VPC has its master updated to 4.14+, then several shared VPE Gateways are created for various IBM Cloud services. Only one of each of these types of shared VPE Gateways is created per VPC. All the clusters in the VPC share the same VPE Gateway for these services. These shared VPE Gateways are assigned a single Reserved IP from each zone that the cluster workers are in.

The following VPE gateways are created automatically when you create a VPC cluster. 

| VPE Gateway | Description |
| --- | --- |
| {{site.data.keyword.registrylong_notm}} | [Shared]{: tag-cool-gray} Pull container images from {{site.data.keyword.registrylong_notm}} to apps running in your cluster. 
| {{site.data.keyword.cos_full_notm}} s3 gateway | [Shared]{: tag-cool-gray} Access the COS APIs. |
| {{site.data.keyword.cos_full_notm}} config gateway | [Shared]{: tag-cool-gray} Backup container images to {{site.data.keyword.cos_full_notm}} |
| {{site.data.keyword.openshiftlong_notm}} | Access the {{site.data.keyword.openshiftlong_notm}} APIs to interact with and manage your cluster. † |
{: caption="Table 1. VPE gateways" caption-side="bottom"}
{: summary="The table shows the VPE gateways created for VPC clusters. The first column includes name of the gateway. The second column includes a brief description."}


† All supported VPC clusters have a VPE Gateway for the cluster master that gets created at in the your account when the cluster gets created. This VPE Gateway is used by the cluster workers, and can be used by other things in the VPC, to connect to the cluster's master API server. This VPE Gateway is assigned a single Reserved IP from each zone that the cluster workers are in, and this IP is created in one of the VPC subnets in that zone that has cluster workers. For example, if the cluster has workers in only a single zone (`us-east-1`) and single VPC subnet, then a single IP is created in that subnet and assigned to the VPE Gateway. If a cluster has workers in all three zones like `us-east-1`, `us-east-2`, and `us-east-3` and these workers are spread out among 4 VPC subnets in each zone, then 12 VPC subnets altogether, three IPs are created, one in each zone, in one of the four VPC subnets in that zone. Note that the subnet is chosen at random.

## Managed security groups
{: #managed-sgs}

### Security groups applied to cluster workers
{: #vpc-sg-cluster-workers}

Do not modify the rules in the`kube-<clusterID>` security group as doing so might cause disruptions in network connectivity between the workers of the cluster and the control cluster. However, if you don't want the `kube-<clusterID>`, you can instead add your own security groups during [cluster creation](/docs/openshift?topic=openshift-cluster-create-vpc-gen2).


| Security group type | Name | Details |
| --- | --- | --- | 
| VPC security group | Randomly generated | - Automatically created when the VPC is created. Automatically attached to each worker node in a cluster created in the VPC.  \n - Allows all outbound traffic by default. |
| VPC cluster security group | `kube-<clusterID>`| - Automatically created when the VPC cluster is created. Automatically attached to each worker node in a cluster created in the VPC.   \n - Allows traffic necessary for the cluster infrastructure to function. |
{: caption="Table 1. VPC security groups" caption-side="bottom"}
{: summary="The table shows the three types of security groups that are automatically created for VPCs. The first column includes the type of security group. The second column includes the naming format of the security group. The third column includes details on when and where the security group is created and what type of traffic it allows."}

### Security groups applied to VPE gateways and VPC ALBs
{: #vpc-sg-vpe-alb}

Do not modify the rules in the `kube-<vpcID>` security group as doing so might cause disruptions in network connectivity between the workers of the cluster and the control cluster. However, you can [remove the default security group from the VPC ALB](/docs/vpc?topic=vpc-vpc-reference#security-group-target-remove) and [replace it with a custom security group](/docs/vpc?topic=vpc-vpc-reference#security-group-target-add) that you create and manage. 


| Security group type | Name | Details |
| --- | --- | --- | 
| {{site.data.keyword.openshiftlong_notm}} security group | `kube-<vpcID>` | - Automatically created and attached to any cluster-related VPE gateways in the VPC.  \n - Automatically created and attached to each VPC ALB that is created in the VPC.  \n - Allows traffic necessary for the cluster infrastructure to function. |
{: caption="Table 1. VPC security groups" caption-side="bottom"}
{: summary="The table shows the three types of security groups that are automatically created for VPCs. The first column includes the type of security group. The second column includes the naming format of the security group. The third column includes details on when and where the security group is created and what type of traffic it allows."}

## Minimum inbound and outbound requirements 
{: #vpc-sg-inbound-outbound}

The following inbound and outbound rules are covered by the default VPC security groups. Note that you can modify the randomly named VPC security group and the cluster-level `kube-<clusterID>` security group, but you must make sure that these rules are still met. 

Modifying the `kube-<vpcID>` security group is not recommended as doing so might cause disruptions in network connectivity between the cluster and the Kubernetes master. Instead, you can [remove the default security group from the VPC ALB or VPE gateway](/docs/vpc-infrastructure-cli-plugin?topic=vpc-infrastructure-cli-plugin-vpc-reference&interface=cli#security-group-target-remove) and [replace it with a security group](/docs/vpc-infrastructure-cli-plugin?topic=vpc-infrastructure-cli-plugin-vpc-reference&interface=cli#security-group-target-add) that you create and manage. 
{: important}

### Required inbound and outbound rules for cluster workers
{: #required-group-rules-workers}

By default, traffic rules for cluster workers are covered by the randomly named VPC security group and the `kube-<clusterID>` cluster security group. If you modify or replace either of these security groups, make sure the following traffic rules are still allowed. 
{: shortdesc}

If you have a VPC cluster that runs at version  or later, you might need to include [additional security group rules](#rules-sg-128). 
{: important}

#### Inbound rules
{: #min-inbound-rules-sg-workers}

| Rule purpose | Protocol | Port or Value | Source |
| --- | --- | --- | --- |
| Allow all worker nodes in this cluster to communicate with each other. | ALL | - | VPC security group `randomly-generated-sg-name` |
| Allow incoming traffic requests to apps that run on your worker nodes. | TCP | `30000` - `32767` | Any |
| If you require VPC VPN access or classic infrastructure access into this cluster, allow incoming traffic requests to apps that run on your worker nodes. | UDP | `30000` - `32767` | Any |
{: caption="Required inbound rules for cluster worker security groups" caption-side="bottom"}


#### Outbound rules
{: #min-outbound-rules-sg-workers}

| Rule purpose | Protocol | Port or Value | Destination |
| --- | --- | --- | --- |
| Allow worker nodes to be created in your cluster. | ALL | - | CIDR block `161.26.0.0/16` |
| Allow worker nodes to communicate with other {{site.data.keyword.cloud_notm}} services that support private cloud service endpoints. | ALL | - | CIDR block `166.8.0.0/14` | 
| Allow all worker nodes in this cluster to communicate with each other. | ALL | - | Security group `kube-<cluster_ID>` |
| Allow outbound traffic to be sent to the Virtual private endpoint gateway which is used to talk to the Kubernetes master. | ALL | - | Virtual private endpoint gateway IP addresses. The Virtual private endpoint gateway is assigned an IP address from a VPC subnet in each of the zones where your cluster has a worker node. For example, if the cluster spans 3 zones, there are up to 3 IP addresses assigned to each Virtual private endpoint gateway. To find the Virtual private endpoint gateway IPs:  \n 1. Go to the [Virtual private cloud dashboard](https://cloud.ibm.com/vpc-ext/network/vpcs){: external}.  \n 2. Click **Virtual private endpoint gateways**, then select the **Region** where your cluster is located.  \n 3. Find your cluster, then click the IP addresses in the **IP Address** column to copy them. |
| Allow the worker nodes to connect to the public service endpoint IPs for the OAuth service. To find the IPs needed to apply this rule, see [Allow the worker nodes to connect to the public service endpoint IPs for the OAuth service](#worker-node-public-service-endpoint-previous). | TCP | OAuth port | OAuth IP addresses |
| Allow the worker nodes to connect to the Ingress LoadBalancer. To find the IPs needed to apply this rule, see [Allow worker nodes to connect to the Ingress LoadBalancer](#vpc-security-group-loadbalancer-outbound). | TCP | 443 | Ingress load balancer IPs |
{: caption="Required outbound rules for cluster worker security groups" caption-side="bottom"}

### Required rules for VPCs with a cluster that runs at version 4.14 or later
{: #rules-sg-128}

In version 1.27 and earlier, VPC clusters pull images from the IBM Cloud Container Registry through a private cloud service endpoint for the Container Registry. For version 4.14 and later, this network path is updated so that images are pulled through a VPE gateway instead of a private service endpoint. This change affects all clusters in a VPC; when you create or update a single cluster in a VPC to version 4.14, all clusters in that VPC, regardless of their version or type, have their network path updated. For more information, see [Networking changes for VPC clusters](/docs/containers?topic=containers-cs_versions_128#networking_128).

If you update or create a cluster in your VPC that runs at version 4.14 or later, you must make sure that the following security group rules are implemented to allow traffic to the VPE gateway for registry. Each of these rules must be created for each zone in the VPC and must specify the entire VPC address prefix range for the zone as the destination CIDR. To find the VPC address prefix range for each zone in the VPC, run `ibmcloud is vpc-address-prefixes <vpc_name_or_id>`.

| Rule type | Protocol | Destination IP or CIDR | Destination Port |
|---|---|---|---|
| Outbound | TCP | Entire VPC address prefix range | 443 |
| Outbound | TCP | Entire VPC address prefix range | 4443 |
{: caption="Outbound security group rules to add for version 4.14" caption-side="bottom"}
{: caption="Required outbound rules for cluster worker security groups" caption-side="bottom"}


### Required inbound and outbound rules for VPC ALBs
{: #required-group-rules-alb}

By default, traffic rules for VPC ALBs are covered by the `kube-<vpcID>` security group. Note that you should not modify this security group as doing so might cause disruptions in network connectivity between the cluster and the Kubernetes master. However, you can [remove the security group](/docs/vpc-infrastructure-cli-plugin?topic=vpc-infrastructure-cli-plugin-vpc-reference&interface=cli#security-group-target-remove) from your ALB and [replace it](/docs/vpc-infrastructure-cli-plugin?topic=vpc-infrastructure-cli-plugin-vpc-reference&interface=cli#security-group-target-add) with one that you create and manage. If you do so, you must make sure that the following traffic rules are still covered. 
{: shortdesc}

#### Inbound rules
{: #min-inbound-rules-sg-alb}

| Rule purpose | Protocol | Port or Value | Source |
| --- | --- | --- | --- |
| If you use your own security group for the LBaaS for Ingress and you expose any applications in your cluster with Ingress, you must allow TCP protocol to ports 443 or 80, or both. You can allow access for all clients, or you can allow only certain source IPs or subnets to access these applications. Note that this requirement also applies if you want to use the OpenShift Console, which is exposed by the cluster's default Ingress instance and router. To allow access for the OpenShift Console, you must allow TCP protocol to port 443 from all sources, or from specific source IP addresses or subnets. | TCP | `80 or 443` | All sources, or specific source IP addresses or subnets |
| If you use your own security group for any LBaaS instances that you use to expose other applications, then within that security group you must allow any intended sources to access the appropriate ports and protocols. | TCP, UDP, or both | LBaaS ports | Any sources, or specific source IPs or subnets |
{: caption="Required inbound rules for VPC ALB security groups" caption-side="bottom"}


#### Outbound rules
{: #min-outbound-rules-sg-alb}

| Rule purpose | Protocol | Port or Value | Destination |
| --- | --- | --- | --- |
| Allow the ALB to send traffic to the cluster workers on the TCP NodePort range | TCP | `30000` - `32767` | Any |
| Allow the ALB to send traffic to the cluster workers on the UDP NodePort range | UDP | `30000` - `32767` | Any |
| If you use your own security group for the LBaaS for Ingress, you must allow TCP traffic from cluster worker nodes to port 443. If you do not already allow all TCP traffic port to 443, such as if you filter traffic by source IP, then allowing traffic from cluster worker nodes is the minimum requirement for the Red Hat OpenShift console operator and Ingress health checks to succeed. | TCP | 443 | Security group `kube-<cluster_ID>` |
{: caption="Required outbound rules for VPE and VPC ALB security groups " caption-side="bottom"}







## Allow the worker nodes to connect to the public service endpoint IPs for the OAuth service
{: #worker-node-public-service-endpoint-previous}

Required for VPC clusters with a public service endpoint.
{: important}

[Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-access_cluster)
1. Get the URL used to connect to the oauth service in the form `https://cXXX-e.<region>.containers.cloud.ibm.com:<PORT>`. Make a note of the region and port.

    ```sh
    oc get --raw /.well-known/oauth-authorization-server | grep issuer
    ```
    {: pre}
    
    Example output
    
    ```sh
    "issuer": "https://c104-e.us-east.containers.cloud.ibm.com:31062",
    ```
    {: screen}
    
2. Run `dig +short` or `nslookup` to get the IPs associated with the hostname in the URL. For single zone regions there is only one public IP associated with the hostname. For multizone regions, there are 3. Look up the individual IPs by replacing `e` with 1, 2, and 3.
    ```sh
    dig +short cXXX-1.<region>.containers.cloud.ibm.com
    dig +short cXXX-2.<region>.containers.cloud.ibm.com
    dig +short cXXX-3.<region>.containers.cloud.ibm.com
    ```
    {: pre}
    
    Example output
    ```sh
    169.63.111.82
    ```
    {: screen}
    
3. Add a security group rule for each of the IPs that allows an outbound TCP connection to the destination IP and PORT.

    ```sh
    ibmcloud is sg-rulec <sg> outbound tcp --port-min 31062 --port-max 31062 --remote 169.63.111.82
    ```
    {: pre}
    
    Example output
    ```sh
    Direction              outbound   
    IP version             ipv4   
    Protocol               tcp   
    Min destination port   31062   
    Max destination port   31062   
    Remote                 169.63.111.82
    ```
    {: screen}




## Allow worker nodes to connect to the Ingress LoadBalancer
{: #vpc-security-group-loadbalancer-outbound}

Follow the steps to allow worker nodes to connect to the Ingress LoadBalancer.
{: shortdesc}

1. Get the `EXTERNAL-IP` of the LoadBalancer service.

    ```sh
    oc get svc -o wide -n openshift-ingress router-default
    ```
    {: pre}

1. Run `dig` on the `EXTERNAL-IP` to get the IP addresses associated with the LoadBalancer.
    ```sh
    dig <EXTERNAL-IP> +short
    ```
    {: pre}
    
    Example output
    ```sh
    150.XXX.XXX.XXX
    169.XX.XXX.XXX
    ```
    {: screen}
    
1. Create outbound security rules to each of the IP address that you retrieved earlier and port 443.
    ```sh
    ibmcloud is sg-rulec <sg> outbound tcp --port-min 443 --port-max 443 --remote 150.XXX.XXX.XXX
    ```
    {: pre}
    
If the Ingress or console operators fail their health checks, you can repeat these steps to see if the LoadBalancer IP addresses changed. While rare, if the amount of traffic to your LoadBalancers varies widely, these IP addresses might change to handle the increased or decreased load.
{: tip}
    





