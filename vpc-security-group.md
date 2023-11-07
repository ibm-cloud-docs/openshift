---

copyright: 
  years: 2014, 2023
lastupdated: "2023-11-07"

keywords: openshift, kubernetes, firewall, acl, acls, access control list, rules, security group

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}





# Controlling traffic with VPC security groups
{: #vpc-security-group}
{: help}
{: support}

[Virtual Private Cloud]{: tag-vpc}

VPC clusters use various security groups to protect cluster components. These security groups are automatically created and attached to cluster workers, load balancers, and cluster-related VPE gateways. You can modify or replace these security groups to meet your specific requirements, however, any modifications must be made according to these guidelines to avoid network connectivity disruptions.
{: shortdesc}

## VPC security groups
{: #vpc-security-groups-details}

Default behavior
:   Virtual Private Cloud security groups filter traffic at the hypervisor level. Security group rules are not applied in a particular order. However, requests to your worker nodes are only permitted if the request matches one of the rules that you specify. When you allow traffic in one direction by creating an inbound or outbound rule, responses are also permitted in the opposite direction. Security groups are additive, meaning that if your worker nodes are attached to more than one security group, all rules included in the security groups are applied to the worker nodes. Newer cluster versions might have more rules in the `kube-clusterID` security group than older cluster versions. Security group rules are added to improve the security of the service and do not break functionality.

Limitations
:   Because the worker nodes of your VPC cluster exist in a service account and aren't listed in the VPC infrastructure dashboard, you can't create a security group and apply it to your worker node instances. You can only modify the existing security group.


If you modify the default VPC security groups, you must, at minimum, include the required [inbound](#min-outbound-rules-sg-workers) and [outbound](#min-inbound-rules-sg-workers) rules so that your cluster works properly.  
{: important}

### Security groups applied to cluster workers
{: #vpc-sg-cluster-workers}

Do not modify the rules in the`kube-<cluster-ID>` security group as doing so might cause disruptions in network connectivity between the workers of the cluster and the control cluster. However, if you don't want the `kube-<cluster-ID>`, you can instead add your own security groups during [cluster creation](/docs/openshift?topic=openshift-cluster-create-vpc-gen2&interface=ui).


| Security group type | Name | Details |
| --- | --- | --- | 
| VPC security group | Randomly generated | - Automatically created when the VPC is created. Automatically attached to each worker node in a cluster created in the VPC.  \n - Allows all outbound traffic by default. |
| VPC cluster security group | `kube-<cluster-ID>`| - Automatically created when the VPC cluster is created. Automatically attached to each worker node in a cluster created in the VPC.   \n - Allows traffic necessary for the cluster infrastructure to function. |
{: caption="Table 1. VPC security groups" caption-side="bottom"}
{: summary="The table shows the three types of security groups that are automatically created for VPCs. The first column includes the type of security group. The second column includes the naming format of the security group. The third column includes details on when and where the security group is created and what type of traffic it allows."}

### Security groups applied to VPE gateways and VPC ALBs
{: #vpc-sg-vpe-alb}

Do not modify the rules in the `kube-<vpc-id>` security group as doing so might cause disruptions in network connectivity between the workers of the cluster and the control cluster. However, you can [remove the default security group from the VPC ALB](/docs/vpc?topic=vpc-vpc-reference#security-group-target-remove) and [replace it with a security group](/docs/vpc?topic=vpc-vpc-reference#security-group-target-add) that you create and manage. 


| Security group type | Name | Details |
| --- | --- | --- | 
| {{site.data.keyword.openshiftlong_notm}} security group | `kube-<vpc-id>` | - Automatically created and attached to any cluster-related VPE gateways in the VPC.  \n - Automatically created and attached to each VPC ALB that is created in the VPC.  \n - Allows traffic necessary for the cluster infrastructure to function. |
{: caption="Table 1. VPC security groups" caption-side="bottom"}
{: summary="The table shows the three types of security groups that are automatically created for VPCs. The first column includes the type of security group. The second column includes the naming format of the security group. The third column includes details on when and where the security group is created and what type of traffic it allows."}


## Viewing VPC security groups in the CLI
{: #vpc-sg-cli}
{: cli}

Follow the steps to view details about the VPC security groups.

1. List your clusters and note the **ID** of the cluster that you are working in.

    To check what VPC a cluster is in, run `ibmcloud oc cluster get --cluster <cluster_name_or_id>` and check the **VPC ID** in the output.
    {: tip}

    ```sh
    ibmcloud oc cluster ls --provider vpc-gen2
    ```
    {: screen}

1. List the security groups attached to the VPC that your cluster is in. The VPC security group is assigned a randomly generated name, such as `trench-hexagon-matriarch-flower`. The VPC cluster security group is named in the format of `kube-<cluster-ID>`. The {{site.data.keyword.openshiftlong_notm}} security group is named in the format of `kube-<vpc-ID>`. 

    ```sh
    ibmcloud is sgs | grep <vpc_name>
    ```
    {: pre}

    Example output.

    ```sh
    ID                                          Name                                             Rules   Network interfaces   VPC                          Resource group   

    r006-111aa1aa-1a1a-1a11-1111-a111aaa1a11a   trench-hexagon-matriarch-flower                    4       0                    my-vpc                      default   
    r006-222aa2aa-2a2a-2a22-2222-a222aaa2a22a   kube-a111a11a11aa1aa11a11                          4       0                    my-vpc                      default   
    r006-333aa3aa-3a3a-3a33-3333-a333aaa3a33a   kube-r006-111a11aa-aaa1-1a1a-aa11-1a1a111aa11      4       0                    my-vpc                      default   
    ```
    {: screen}

1. Get the details of a security group. Find the **Rules** section in the output to view the inbound and outbound rules attached to the security group.

    ```sh
    ibmcloud is sg <security-group-name>
    ```
    {: pre}

    Example output.

    ```sh
    ...
    Rules      
    ID                                          Direction   IP version   Protocol                  Remote   
    r006-111bb1bb-1b1b-1b11-1111-b111bbb1b11b   outbound    ipv4         all                       0.0.0.0/0   
    r006-222bb2bb-2b2b-2b22-2222-b222bbb2b22b   inbound     ipv4         all                       behind-unbuilt-guidable-anthill   
    r006-333bb3bb-3b3b-3b33-3333-b333bbb3b33b   inbound     ipv4         icmp Type=8               0.0.0.0/0   
    r006-444bb4bb-4b4b-4b44-4444-b444bbb4b44b   inbound     ipv4         tcp Ports:Min=22,Max=22   0.0.0.0/0 
    ```
    {: screen}

## Viewing the default VPC security groups in the UI
{: #vpc-sg-ui}
{: ui}

1. From the [Security groups for VPC dashboard](https://cloud.ibm.com/vpc-ext/network/securityGroups){: external}, find the security groups that are attached to the VPC that your cluster is in. The VPC cluster security group is named in the format of `kube-<cluster-ID>`. The {{site.data.keyword.openshiftlong_notm}} security group is named in the format of `kube-<vpc-ID>`. Click on the security group.

    To sort the security groups by the VPC they are attached to, click the **Virtual Private Cloud** column heading in the table. 
    {: tip}

2. To view the inbound and outbound rules attached to the security group, click the **Rules** tab.

## Minimum inbound and outbound requirements 
{: #vpc-sg-inbound-outbound}

The following inbound and outbound rules are covered by the default VPC security groups. Note that you can modify the randomly named VPC security group and the cluster-level `kube-<cluster-id>` security group, but you must make sure that these rules are still met. 

Modifying the `kube-<vpc-id>` security group is not recommended as doing so might cause disruptions in network connectivity between the cluster and the Kubernetes master. Instead, you can [remove the default security group from the VPC ALB or VPE gateway](/docs/vpc-infrastructure-cli-plugin?topic=vpc-infrastructure-cli-plugin-vpc-reference&interface=cli#security-group-target-remove) and [replace it with a security group](/docs/vpc-infrastructure-cli-plugin?topic=vpc-infrastructure-cli-plugin-vpc-reference&interface=cli#security-group-target-add) that you create and manage. 
{: important}

### Required inbound and outbound rules for cluster workers
{: #required-group-rules-workers}

By default, traffic rules for cluster workers are covered by the randomly named VPC security group and the `kube-<cluster-id>` cluster security group. If you modify or replace either of these security groups, make sure the following traffic rules are still allowed. 
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
| Allow the worker nodes to connect to the public service endpoint IPs for the OAuth service. To find the IPs needed to apply this rule, see [Allow the worker nodes to connect to the public service endpoint IPs for the OAuth service](#worker-node-public-service-endpoint). | TCP | OAuth port | OAuth IP addresses |
| Allow the worker nodes to connect to the Ingress LoadBalancer. To find the IPs needed to apply this rule, see [Allow worker nodes to connect to the Ingress LoadBalancer](#vpc-security-group-loadbalancer-outbound). | TCP | 443 | Ingress load balancer IPs |
{: caption="Required outbound rules for cluster worker security groups" caption-side="bottom"}

### Required rules for VPCs with a cluster that runs at version  or later
{: #rules-sg-128}

In version 1.27 and earlier, VPC clusters pull images from the IBM Cloud Container Registry through a private cloud service endpoint for the Container Registry. For version  and later, this network path is updated so that images are pulled through a VPE gateway instead of a private service endpoint. This change affects all clusters in a VPC; when you create or update a single cluster in a VPC to version , all clusters in that VPC, regardless of their version or type, have their network path updated. For more information, see [Networking changes for VPC clusters](/docs/containers?topic=containers-cs_versions_128&interface=ui#networking_128).

If you update or create a cluster in your VPC that runs at version  or later, you must make sure that the following security group rules are implemented to allow traffic to the VPE gateway for registry. Each of these rules must be created for each zone in the VPC and must specify the entire VPC address prefix range for the zone as the destination CIDR. To find the VPC address prefix range for each zone in the VPC, run `ibmcloud is vpc-address-prefixes <vpc_name_or_id>`.

| Rule type | Protocol | Destination IP or CIDR | Destination Port |
|---|---|---|---|
| Outbound | TCP | Entire VPC address prefix range | 443 |
| Outbound | TCP | Entire VPC address prefix range | 4443 |
{: caption="Outbound security group rules to add for version " caption-side="bottom"}
{: caption="Required outbound rules for cluster worker security groups" caption-side="bottom"}


### Required inbound and outbound rules for VPC ALBs
{: #required-group-rules-alb}

By default, traffic rules for VPC ALBs are covered by the `kube-<vpc-id>` security group. Note that you should not modify this security group as doing so might cause disruptions in network connectivity between the cluster and the Kubernetes master. However, you can [remove the security group](/docs/vpc-infrastructure-cli-plugin?topic=vpc-infrastructure-cli-plugin-vpc-reference&interface=cli#security-group-target-remove) from your ALB and [replace it](/docs/vpc-infrastructure-cli-plugin?topic=vpc-infrastructure-cli-plugin-vpc-reference&interface=cli#security-group-target-add) with one that you create and manage. If you do so, you must make sure that the following traffic rules are still covered. 
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


## Creating security group rules 
{: #vpc-sg-create-rules}

You can add inbound and outbound rules to the default VPC security groups. If you modify the randomly named VPC security group and the cluster-level `kube-<cluster-id>` security group or replace the `kube-<vpc-id>` security group, you must make sure that the [minimum inbound and outbound rules](#vpc-sg-inbound-outbound) are still met. Do not modify the `kube-<vpc-id>` security group itself.
{: shortdesc}

### Creating rules in the console
{: #security-group-inbound-rules}
{: ui}

1. From the [Virtual private cloud dashboard](https://cloud.ibm.com/vpc-ext/network/vpcs){: external}, click the name of the **Default Security Group** for the VPC that your cluster is in.
1. Click the **Rules** tab.
    *  To create new inbound rules to control inbound traffic to your worker nodes, in the **Inbound rules** section, click **Create**. 
    * To create new rules to control outbound traffic to your worker nodes, in the **Outbound rules** section, delete the default rule that allows all outbound traffic. Then, in the **Outbound rules** section, click **Create**. 

Keep in mind that in addition to any rules you create, you must also create the required [inbound and outbound rules](#vpc-sg-inbound-outbound).
{: note}


### Creating rules in the command line
{: #security_groups_cli}
{: cli}

Use the {{site.data.keyword.cloud_notm}} CLI to add inbound and outbound rules to the default security group for your cluster.
{: shortdesc}

1. Install the `infrastructure-service` plug-in. The prefix for running commands is `ibmcloud is`.
    ```sh
    ibmcloud plugin install infrastructure-service
    ```
    {: pre}

1. Target the region that your VPC is in.
    ```sh
    ibmcloud target -r <region>
    ```
    {: pre}

1. Get your cluster's **ID**.
    ```sh
    ibmcloud oc cluster get -c <cluster_name>
    ```
    {: pre}

1. List your security groups and note the **ID** of the default security group for your **VPC**. Note that the default security group uses a randomly generated name and **not** the format `kube-<cluster_ID>`.
    ```sh
    ibmcloud is sgs
    ```
    {: pre}

    Example output with the default security group for the VPC of a randomly generated name, `chamomile-dislodge-showier-unfilled`.
    ```sh
    ID                                          Name                                       Rules   Network interfaces   VPC          Resource group
    1a111a1a-a111-11a1-a111-111111111111        chamomile-dislodge-showier-unfilled        5       2                    events-vpc   default
    2b222b2b-b222-22b2-b222-222222222222        kube-df253b6025d64744ab99ed63bb4567b6      5       3                    gen2-vpn     default
    ```
    {: screen}

1. Store the security group ID as an environment variable.
    ```sh
    sg=<security_group_ID>
    ```
    {: pre}

1. Review the default rules for the security group. Keep in mind that in addition to any rules you create, you must also create the required [inbound and outbound rules](#vpc-sg-inbound-outbound).
    ```sh
    ibmcloud is sg $sg
    ```
    {: pre}

    * To create inbound traffic rules, use the [`ibmcloud is security-group-rule-add <sg> inbound` command](/docs/vpc?topic=vpc-vpc-reference#security-group-rule-add).
        ```sh
        ibmcloud is security-group-rule-add $sg inbound <protocol> [--remote <remote_address> | <CIDR_block> | <security_group_ID>] [--icmp-type <icmp_type> [--icmp-code <icmp_code>]] [--port-min <port_min>] [--port-max <port_max>]
        ```
        {: pre}
        
        
    * To create outbound traffic rules, use the [`ibmcloud is security-group-rule-add <sg> outbound` command](/docs/vpc?topic=vpc-vpc-reference#security-group-rule-add).

        ```sh
        ibmcloud is security-group-rule-add $sg outbound <protocol> [--remote <remote_address> | <CIDR_block> | <security_group_ID>] [--icmp-type <icmp_type> [--icmp-code <icmp_code>]] [--port-min <port_min>] [--port-max <port_max>]
        ```
        {: pre}
        
        1. After you create custom outbound rules, get the ID of the default rule that allows all outbound traffic.

            ```sh
            ibmcloud is sg $sg
            ```
            {: pre}

            Example output
            ```sh
            Rules
            ID                                          Direction   IP version   Protocol                        Remote
            r010-e3a34cbb-d5e8-4713-a57e-3e35a7458272   inbound     ipv4         all                             freeload-flavored-surging-repaying
            r010-036c3a13-1c16-4425-9667-a4ec34b1702b   inbound     ipv4         icmp Type=8                     0.0.0.0/0
            r010-15591636-6976-493f-a94f-70721702860a   inbound     ipv4         tcp Ports:Min=22,Max=22         0.0.0.0/0
            ```
            {: screen}

        1. Delete the default rule that allows all outbound traffic.

            ```sh
            ibmcloud is security-group-rule-delete $sg <rule_ID>
            ```
            {: pre}
    

Keep in mind that in addition to any rules you create, you must also create the required [inbound and outbound rules](#vpc-sg-inbound-outbound).
{: note}

## Adding VPC security groups to clusters and worker pools during create time
{: #vpc-sg-cluster}

When you create a new VPC cluster, the default VPC security group, which has a randomly generated name, and the cluster security group, named `kube-<cluster-id>`, are automatically created and applied to all workers in the cluster. When you create your VPC cluster, you can also attach additional security groups alongside, or instead of, the default VPC security groups. The security groups applied to the workers in the cluster are a combination of the security groups applied when you create the cluster and [when you create the worker pool](#vpc-sg-worker-pool). A total of five security groups can be applied to workers, including the default security groups and any security groups applied to the worker pool. Note that these security group options are only available in the CLI. 
{: shortdesc}

The security groups applied to a cluster cannot be changed once the cluster is created. You can [change the rules of the security groups](/docs/openshift?topic=openshift-vpc-security-group#vpc-sg-create-rules) that are applied to the cluster, but you cannot add or remove security groups at the cluster level. If you apply the incorrect security groups at cluster create time, you must delete the cluster and create a new one. 
{: important}

### If you only want the default VPC and cluster security groups and no additional security groups
{: #default-sgs-only}

[VPC security group]{: tag-blue} [Cluster security group]{: tag-green}

Note that this is the default behavior at cluster create time.
{: note}

When you create your cluster, do not specify any additional security groups. 

Example command to create a VPC cluster with only the default VPC and `kube-<cluster-id>` cluster security groups:

```sh
 ibmcloud oc cluster create vpc-gen2 --name <cluster-name> --zone <zone> --vpc-id <vpc-id> --subnet-id <subnet-id>
```
{: pre}

The following security groups are applied:
- Default VPC security group (randomly generated name)
- `kube-<cluster-id>`

### If you only want the cluster security group and not the default VPC security group
{: #cluster-sg-only}

[Cluster security group]{: tag-green}

When you create the cluster specify `--cluster-security-group cluster`. Do not specify any additional security groups.

Example command to create a VPC cluster with only the `kube-<cluster-id>` cluster security group:

```sh
 ibmcloud oc cluster create vpc-gen2 --name <cluster-name> --zone <zone> --vpc-id <vpc-id> --subnet-id <subnet-id> --cluster-security-group cluster
```
{: pre}

The cluster `kube-<cluster-id>` security group is applied. 
 
### If you want the cluster security group and your own additional security groups
{: #cluster-customer-sgs} 

[Cluster security group]{: tag-green} [Your own security groups]{: tag-warm-gray}

When you create the cluster, specify `--cluster-security-group cluster` and up to four additional security groups that you own. You must include a separate `--cluster-security-group` option for each individual security group you want to add. Note that at maximum of five security groups can be applied to workers, including the security groups that are applied by default. 

Example command to create a VPC cluster with the `kube-<cluster-id>` cluster security group and your own additional security groups:
```sh
 ibmcloud oc cluster create vpc-gen2 --name <cluster-name> --zone <zone> --vpc-id <vpc-id> --subnet-id <subnet-id> --cluster-security-group cluster --cluster-security-group <group-id-1> --cluster-security-group <group-id-2> --cluster-security-group <group-id-3>
```
{: pre}

The following security groups are applied:
- `kube-<cluster-id>`
- Up to four of your own additional security groups, for a maximum of five total security groups. 

### If you only want your own security groups 
{: #customer-sgs-only}

[Your own security groups]{: tag-warm-gray}

When you create the cluster, specify up to five security groups that you own. You must include a separate `--cluster-security-group` option for each individual security group you want to add. 

Example command to create a VPC cluster with only your own security groups:
```sh
 ibmcloud oc cluster create vpc-gen2 --name <cluster-name> --zone <zone> --vpc-id <vpc-id> --subnet-id <subnet-id> --cluster-security-group <group-id-1> --cluster-security-group <group-id-2> --cluster-security-group <group-id-3>
```
{: pre}

Up to five of your own security groups are applied to the workers on the cluster. 

## Adding security groups to worker pools at worker pool create time 
{: #vpc-sg-worker-pool}

By default, the security groups applied to a worker pool are the same security groups that are indicated at cluster create time. However, you can specify additional security groups to apply to a worker pool. If you apply additional security groups to the worker pool, then the security group applied to the workers on the cluster is a combination of the [security groups applied at cluster create](#vpc-sg-cluster) and the security groups applied to the worker pool. 

A maximum of five security groups can be applied to a worker, including the security groups applied by default.
{: note} 

The security groups applied to a worker pool cannot be changed once the worker pool is created. You can change the rules of the security groups that are applied to the worker pool, but you cannot add or remove security groups at the worker pool level. If you apply the incorrect security groups at worker pool create time, you must delete the worker pool and create a new one. 
{: important}

### If you do not want to attach additional security groups to the worker pool
{: #no-worker-sgs}

When you create the worker pool, do not specify any additional security groups.

Example command to create a worker pool with no security groups applied:
```sh
ibmcloud oc worker-pool create vpc-gen2 --name <worker_pool_name> --cluster <cluster_name_or_ID> --flavor <flavor> --size-per-zone <number_of_workers_per_zone> 
```
{: pre}

Only the security groups applied to the cluster are applied to the workers.

### If you do want to attach additional security groups to the worker pool
{: #worker-sgs}

When you create the worker pool specify additional security groups at worker pool create time. You must include a separate `--security-group` option for each individual security group you want to add.

Example command to create a worker pool with your own security groups applied:
```sh
ibmcloud oc worker-pool create vpc-gen2 --name <worker_pool_name> --cluster <cluster_name_or_ID> --flavor <flavor> --size-per-zone <number_of_workers_per_zone> --security-group <group-id-1> --security-group <group-id-2> --security-group <group-id-3>
```
{: pre}

The security groups applied to the workers in the worker pool are a combination of those applied to the cluster that the worker pool is attached to and those applied to the worker pool at create time.





## Allow the worker nodes to connect to the public service endpoint IPs for the OAuth service
{: #worker-node-public-service-endpoint}

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
    ibmcloud is security-group-rule-add <sg> outbound tcp --port-min 31062 --port-max 31062 --remote 169.63.111.82
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
    ibmcloud is security-group-rule-add <sg> outbound tcp --port-min 443 --port-max 443 --remote 150.XXX.XXX.XXX
    ```
    {: pre}
    
If the Ingress or console operators fail their health checks, you can repeat these steps to see if the LoadBalancer IP addresses changed. While rare, if the amount of traffic to your LoadBalancers varies widely, these IP addresses might change to handle the increased or decreased load.
{: tip}
    





