---

copyright: 
  years: 2014, 2022
lastupdated: "2022-02-22"

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

{{site.data.keyword.openshiftshort}} version 4.5 or later
:   The default security group for the VPC is applied to your worker nodes. This security group allows incoming ICMP packets (pings) and incoming traffic from other worker nodes in your cluster.
:   Additionally, a unique security group that is named in the format `kube-<cluster_ID>` is automatically created and applied to the worker nodes for that cluster. This security group allows incoming traffic requests to the 30000 - 32767 port range on your worker nodes, and ensures that all inbound and outbound traffic to the pod subnet is permitted so that worker nodes can communicate with each other across subnets.

Use case
:   Add rules to a security group to manage the inbound and outbound traffic to your VPC cluster. 

{{site.data.keyword.openshiftshort}} version 4.5 or later:
:   Modify the default security group that is applied to the entire VPC (not unique to your cluster).
:   Do **not** modify or delete the unique `kube-<cluster_ID>` security group that is automatically created for the cluster.

Limitations
:   Because the worker nodes of your VPC cluster exist in a service account and aren't listed in the VPC infrastructure dashboard, you can't create a security group and apply it to your worker node instances. You can only modify the existing security group.

For more information, see the [VPC documentation](/docs/vpc?topic=vpc-using-security-groups){: external}.

Keep in mind that in addition to any rules you create, you must also create the required [inbound](#security-group-inbound-rules) and [outbound](#security-group-outbound-rules) rules.
{: note}

## Creating security group rules from the console
{: #security_groups_ui}

Use the {{site.data.keyword.cloud_notm}} console to add inbound and outbound rules to the default security group for your cluster.
{: shortdesc}


### Creating inbound rules in the console
{: #security-group-inbound-rules}

1. From the [Virtual private cloud dashboard](https://cloud.ibm.com/vpc-ext/network/vpcs){: external}, click the name of the **Default Security Group** for the VPC that your cluster is in.
1. Click the **Rules** tab.
    1. To create new inbound rules to control inbound traffic to your worker nodes, in the **Inbound rules** section, click **Create**. 
    1. To create new rules to control outbound traffic to your worker nodes, in the **Outbound rules** section, delete the default rule that allows all outbound traffic.
    1. In the **Outbound rules** section, click **Create**. 

Keep in mind that in addition to any rules you create, you must also create the required [inbound](#security-group-inbound-rules) and [outbound](#security-group-outbound-rules) rules.
{: note}


### Creating security group rules with the CLI
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

1. Review the default rules for the security group.
    ```sh
    ibmcloud is sg $sg
    ```
    {: pre}

### Creating inbound rules by using the command line
{: #security-group-inbound-cli}

1. To create new rules to control inbound traffic to your worker nodes, use the [`ibmcloud is security-group-rule-add` command](/docs/vpc?topic=vpc-infrastructure-cli-plugin-vpc-reference#security-group-rule-add).
    ```sh
    ibmcloud is security-group-rule-add $sg inbound <protocol> [--remote <remote_address> | <CIDR_block> | <security_group_ID>] [--icmp-type <icmp_type> [--icmp-code <icmp_code>]] [--port-min <port_min>] [--port-max <port_max>]
    ```
    {: pre}
    
Keep in mind that in addition to any rules you create, you must also create the required [inbound](#security-group-inbound-rules) and [outbound](#security-group-outbound-rules) rules.
{: note}

### Creating outbound rules by using the command line
{: #security-group-cli-outbound}

1. To create rules to control outbound traffic to your worker nodes, get the ID of the default rule that allows all outbound traffic.

    ```sh
    ibmcloud is sg $sg
    ```
    {: pre}

    In this example output, the outbound rule that allows all outbound traffic to all destinations (`0.0.0.0/0`) is `r010-93ae3092-cce1-4b89-894c-204e628cf8f3`.
    ```sh
    Rules
    ID                                          Direction   IP version   Protocol                        Remote
    r010-93ae3092-cce1-4b89-894c-204e628cf8f3   outbound    ipv4         all                             0.0.0.0/0
    r010-e3a34cbb-d5e8-4713-a57e-3e35a7458272   inbound     ipv4         all                             freeload-flavored-surging-repaying
    r010-036c3a13-1c16-4425-9667-a4ec34b1702b   inbound     ipv4         icmp Type=8                     0.0.0.0/0
    r010-15591636-6976-493f-a94f-70721702860a   inbound     ipv4         tcp Ports:Min=22,Max=22         0.0.0.0/0
    r010-5547cb84-4829-475c-8bdf-be1a39d7936d   inbound     ipv4         tcp Ports:Min=30000,Max=32767   0.0.0.0/0
    ```
    {: screen}

1. Delete the default rule that allows all outbound traffic.

    ```sh
    ibmcloud is security-group-rule-delete $sg <rule_ID>
    ```
    {: pre}

1. Create new rules to control outbound traffic from your worker nodes.

    ```sh
    ibmcloud is security-group-rule-add $sg outbound <protocol> [--remote <remote_address> | <CIDR_block> | <security_group_ID>] [--icmp-type <icmp_type> [--icmp-code <icmp_code>]] [--port-min <port_min>] [--port-max <port_max>]
    ```
    {: pre}
    
Keep in mind that in addition to any rules you create, you must also create the required [inbound](#security-group-inbound-rules) and [outbound](#security-group-outbound-rules) rules.
{: note}


    
    
## Required inbound rules
{: #security-group-inbound-rules}

| Rule purpose | Protocol | Port or Value | Type |
| --- | --- | --- | --- |
| Allow all worker nodes in this cluster to communicate with each other. | ALL | - | Security group `<SG_name>` |
| {{site.data.keyword.openshiftshort}} version < 4.5: Allow incoming traffic requests to apps that run on your worker nodes. | TCP | `30000` - `32767` | Any |
| {{site.data.keyword.openshiftshort}} version < 4.5: If you require VPC VPN access or classic infrastructure access into this cluster, allow incoming traffic requests to apps that run on your worker nodes. | UDP | `30000` - `32767` | Any |
| `*` For Classic clusters, allow access from the {{site.data.keyword.openshiftshort}} control plane IP addresses that are used to health check and report the overall status of your Ingress components. Create one rule for each [control plane CIDR for the region where your cluster is located](https://github.com/IBM-Cloud/kube-samples/tree/master/control-plane-ips){: external}. For VPC clusters, if you use your own security group to the LBaaS for Ingress, set port 80 to allow access from the {{site.data.keyword.openshiftshort}} control plane IP addresses. | TCP | `80` | Each [control plane CIDR for the region where your cluster is located](https://github.com/IBM-Cloud/kube-samples/tree/master/control-plane-ips){: external}. |
{: caption="Table 2. Required inbound rules" caption-side="top"}
{: summary="The table shows required inbound connectivity rules for your VPC security group. Rows are read from the left to right, with the purpose of the rule in column one, the protocol in column two, the required ports or values for the protocol in column in three, and the source type and a brief description of the service in column two."}

`*` Alternatively, to allow the inbound traffic for router health checks, you can create a single rule to allow all incoming traffic on port 80.



## Required outbound rules
{: #security-group-outbound-rules}

| Rule purpose | Protocol | Port or Value | Source type |
| --- | --- | --- | --- |
| Allow worker nodes to be created in your cluster. | ALL | - | CIDR block `161.26.0.0/16` |
| Allow worker nodes to communicate with other {{site.data.keyword.cloud_notm}} services that support private cloud service endpoints, and in clusters that run  with the cluster master through the private cloud service endpoint. | ALL | - | CIDR block `166.8.0.0/14` | 
| Allow all worker nodes in this cluster to communicate with each other. | ALL | - | Security group `kube-<cluster_ID>` |
| Allow outbound traffic to be sent to the Virtual private endpoint gateway which is used to talk to the Kubernetes master. | ALL | - | Virtual private endpoint gateway IP addresses. The Virtual private endpoint gateway is assigned an IP address from a VPC subnet in each of the zones where your cluster has a worker node. For example, if the cluster spans 3 zones, there are up to 3 IP addresses assigned to each Virtual private endpoint gateway. To find the Virtual private endpoint gateway IPs:  \n 1. Go to the [Virtual private cloud dashboard](https://cloud.ibm.com/vpc-ext/network/vpcs){: external}.  \n 2. Click **Virtual private endpoint gateways**, then select the **Region** where you cluster is located.  \n 3. Find your cluster, then click the IP addresses in the **IP Address** column to copy them. |
{: caption="Table 4. Required outbound rules" caption-side="top"}
{: summary="The table shows required outbound connectivity rules for your VPC security group. Rows are read from the left to right, with the purpose of the rule in column one, the protocol in column two, the required ports or values for the protocol in column in three, and the source type and a brief description of the service in column two."}

Verify your security group rules by running the `ibmcloud is sg $sg` command.
{: tip}




