---

copyright: 
  years: 2014, 2022
lastupdated: "2022-03-10"

keywords: openshift, firewall, acl, acls, access control list, rules, security group

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Controlling traffic with the default security group
{: #vpc-security-group}
{: help}
{: support}

Control inbound and outbound traffic to your worker nodes by modifying a VPC security group.
{: shortdesc}

The default rules of the security group for your cluster differs with your cluster version.
{: note}

Level of application
:   Worker node

Default behavior
:   VPC security groups filter traffic at the hypervisor level. Security group rules are not applied in a particular order. However, requests to your worker nodes are only permitted if the request matches one of the rules that you specify. When you allow traffic in one direction by creating an inbound or outbound rule, responses are also permitted in the opposite direction. Security groups are additive, meaning that if your worker nodes are attached to more than one security group, all rules included in the security groups are applied to the worker nodes.
:   The default security group for the VPC is applied to your worker nodes. This security group allows incoming ICMP packets (pings) and incoming traffic from other worker nodes in your cluster.
:   Additionally, a unique security group that is named in the format `kube-<cluster_ID>` is automatically created and applied to the worker nodes for that cluster. This security group allows incoming traffic requests to the 30000 - 32767 port range on your worker nodes, and ensures that all inbound and outbound traffic to the pod subnet is permitted so that worker nodes can communicate with each other across subnets.

Limitations
:   Because the worker nodes of your VPC cluster exist in a service account and aren't listed in the VPC infrastructure dashboard, you can't create a security group and apply it to your worker node instances. You can only modify the existing security group.

If you modfiy the default VPC security group, you must, at minumum, include the required [inbound](#security-group-inbound-rules) and [outbound](#security-group-outbound-rules) rules so that your cluster works properly.
{: important}

For more information about security groups, see the [VPC documentation](/docs/vpc?topic=vpc-using-security-groups){: external}.
{: tip}




## Required inbound rules
{: #required-group-inbound-rules}

| Rule purpose | Protocol | Port or Value | Type |
| --- | --- | --- | --- |
| Allow all worker nodes in this cluster to communicate with each other. | ALL | - | Security group `<SG_name>` |
| Allow incoming traffic requests to apps that run on your worker nodes. | TCP | `30000` - `32767` | Any |
| If you require VPC VPN access or classic infrastructure access into this cluster, allow incoming traffic requests to apps that run on your worker nodes. | UDP | `30000` - `32767` | Any |
{: caption="Table 2. Required inbound rules" caption-side="top"}
{: summary="The table shows required inbound connectivity rules for your VPC security group. Rows are read from the left to right, with the purpose of the rule in column one, the protocol in column two, the required ports or values for the protocol in column in three, and the source type and a brief description of the service in column two."}


## Required outbound rules
{: #security-group-outbound-rules}

| Rule purpose | Protocol | Port or Value | Source type |
| --- | --- | --- | --- |
| Allow worker nodes to be created in your cluster. | ALL | - | CIDR block `161.26.0.0/16` |
| Allow worker nodes to communicate with other {{site.data.keyword.cloud_notm}} services that support private cloud service endpoints. | ALL | - | CIDR block `166.8.0.0/14` | 
| Allow all worker nodes in this cluster to communicate with each other. | ALL | - | Security group `kube-<cluster_ID>` |
| Allow outbound traffic to be sent to the Virtual private endpoint gateway which is used to talk to the Kubernetes master. | ALL | - | Virtual private endpoint gateway IP addresses. The Virtual private endpoint gateway is assigned an IP address from a VPC subnet in each of the zones where your cluster has a worker node. For example, if the cluster spans 3 zones, there are up to 3 IP addresses assigned to each Virtual private endpoint gateway. To find the Virtual private endpoint gateway IPs:  \n 1. Go to the [Virtual private cloud dashboard](https://cloud.ibm.com/vpc-ext/network/vpcs){: external}.  \n 2. Click **Virtual private endpoint gateways**, then select the **Region** where you cluster is located.  \n 3. Find your cluster, then click the IP addresses in the **IP Address** column to copy them. |
| Allow the worker nodes to connect to the public service endpoint IPs for the OAuth service. To find the IPs needed to apply this rule, see [Allow the worker nodes to connect to the public service endpoint IPs for the OAuth service](#worker-node-public-service-endpoint). | TCP | 443 | Security group `kube-<cluster_ID>` |
| Allow the worker nodes to connect to the public LoadBalancer. To find the IPs needed to apply this rule, see [Allow worker nodes to connect to the public LoadBalancer](#vpc-security-group-loadbalancer-outbound). | TCP | 443 | Security group `kube-<cluster_ID>` service |
{: caption="Table 4. Required outbound rules" caption-side="top"}
{: summary="The table shows required outbound connectivity rules for your VPC security group. Rows are read from the left to right, with the purpose of the rule in column one, the protocol in column two, the required ports or values for the protocol in column in three, and the source type and a brief description of the service in column two."}

## Creating inbound and outbound rules in the console
{: #security-group-inbound-rules}

1. From the [Virtual private cloud dashboard](https://cloud.ibm.com/vpc-ext/network/vpcs){: external}, click the name of the **Default Security Group** for the VPC that your cluster is in.
1. Click the **Rules** tab.
    *  To create new inbound rules to control inbound traffic to your worker nodes, in the **Inbound rules** section, click **Create**. 
    * To create new rules to control outbound traffic to your worker nodes, in the **Outbound rules** section, delete the default rule that allows all outbound traffic. Then, in the **Outbound rules** section, click **Create**. 

Keep in mind that in addition to any rules you create, you must also create the required [inbound](#security-group-inbound-rules) and [outbound](#security-group-outbound-rules) rules.
{: note}


## Creating security group rules in the command line
{: #security_groups_cli}

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

1. Review the default rules for the security group. Keep in mind that in addition to any rules you create, you must also create the required [inbound](#security-group-inbound-rules) and [outbound](#security-group-outbound-rules) rules.
    ```sh
    ibmcloud is sg $sg
    ```
    {: pre}

    * To create inbound traffic rules, use the [`ibmcloud is security-group-rule-add <sg> inbound` command](/docs/vpc?topic=vpc-infrastructure-cli-plugin-vpc-reference#security-group-rule-add).
        ```sh
        ibmcloud is security-group-rule-add $sg inbound <protocol> [--remote <remote_address> | <CIDR_block> | <security_group_ID>] [--icmp-type <icmp_type> [--icmp-code <icmp_code>]] [--port-min <port_min>] [--port-max <port_max>]
        ```
        {: pre}
        
        
    * To create outbound traffic rules, use the [`ibmcloud is security-group-rule-add <sg> outbound` command](/docs/vpc?topic=vpc-infrastructure-cli-plugin-vpc-reference#security-group-rule-add).

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
    
Keep in mind that in addition to any rules you create, you must also create the required [inbound](#security-group-inbound-rules) and [outbound](#security-group-outbound-rules) rules.
{: note}



## Allow the worker nodes to connect to the public service endpoint IPs for the OAuth service
{: #worker-node-public-service-endpoint}

Required for VPC clusters with a public service endpoint.
{: important}

[Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)
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


## Allow worker nodes to connect to the public LoadBalancer
{: #vpc-security-group-loadbalancer-outbound}

Required for VPC clusters with a public service endpoint.
{: important}

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
    
If the {{site.data.keyword.redhat_openshift_notm}} Ingress or console operators fail their health checks, you can repeat these steps to see if the LoadBalancer IPs changed. Note that these IPs might change after updating your cluster master. While rare, if the amount of traffic to your LoadBalancers varies widely, these IPs might change to handle the increased or decreased load.
{: tip}



    
    












