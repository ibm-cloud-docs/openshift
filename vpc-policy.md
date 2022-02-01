---

copyright: 
  years: 2014, 2022
lastupdated: "2022-02-01"

keywords: openshift, firewall, acl, acls, access control list, rules, security group

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# VPC: Controlling traffic with ACLs, security groups, and network policies
{: #vpc-network-policy}

![VPC infrastructure provider icon.](images/icon-vpc-2.svg) This information is specific to VPC clusters. For network policy information for classic clusters, see [Classic: Controlling traffic with network policies](/docs/containers?topic=containers-network_policies).
{: note}

Control traffic to and from your cluster and traffic between pods in your cluster by creating network rules and policies.
{: shortdesc}

## Overview
{: #overview}

Control traffic to and from your cluster with VPC access control lists (ACLs) and VPC security groups, and control traffic between pods in your cluster with Kubernetes network policies.
{: shortdesc}

### Comparison of network security options
{: #comparison}

The following table describes the basic characteristics of each network security option that you can use for your VPC cluster in {{site.data.keyword.openshiftlong_notm}}.
{: shortdesc}

|Policy type|Application level|Default behavior|Use case|Limitations|
|-----------|-----------------|----------------|--------|-----------|
|[VPC security groups](#security_groups) (Recommended)|Worker node|Version 4.5 and later: The default security groups for your cluster allow incoming traffic requests to the 30000 - 32767 port range on your worker nodes.</br>Version 4.4 and earlier: The default security group for your VPC denies all incoming traffic requests to your worker nodes.|Control inbound and outbound traffic to and from your worker nodes. Rules allow or deny traffic to or from an IP range with specified protocols and ports. |You can add rules to the default security group that is applied to your worker nodes. However, because your worker nodes exist in a service account and are not listed in the VPC infrastructure dashboard, you can't add more security groups and apply them to your worker nodes.|
|[VPC security groups](/docs/vpc?topic=vpc-alb-integration-with-security-groups)|Load balancer|If you don't specify a security group when you create a load balancer, then the default security group is used.|Allow inbound traffic from all sources to the listener port on a public load balancer.|None|
|[VPC access control lists (ACLs)](#acls) (Not recommended)|VPC subnet|The default ACL for the VPC, `allow-all-network-acl-<VPC_ID>`, allows all traffic to and from your subnets. Changing the default ACL is not recommended; instead, use security groups.|Control inbound and outbound traffic to and from the cluster subnet that you attach the ACL to. Rules allow or deny traffic to or from an IP range with specified protocols and ports.|can't be used to control traffic between the clusters that share the same VPC subnets. Instead, you can [create Calico policies](/docs/openshift?topic=openshift-network_policies#isolate_workers) to isolate your clusters on the private network.|
|[Kubernetes network policies](#kubernetes_policies)|Worker node host endpoint|None|Control traffic within the cluster at the pod level by using pod and namespace labels. Protect pods from internal network traffic, such as isolating app microservices from each other within a namespace or across namespaces.|None|
{: caption="Network security options for VPC clusters"}

VPC Load Balancer also supports security groups. For more information, see [Integrating an IBM Cloud Application Load Balancer for VPC with security groups](/docs/vpc?topic=vpc-alb-integration-with-security-groups).
{: note}


### Do I use ACLs or security groups?
{: #acl-sg-compare}

Although you can use either VPC ACLs or VPC security groups to control inbound traffic to and outbound traffic from your cluster, security groups are easier to implement. You can simplify your security setup by adding rules to only the default security group for your cluster, and leaving the default ACL for your VPC as-is.
{: shortdesc}

To simplify your VPC security setup, leave your default ACL for the VPC as-is. If you configure rules in both ACLs for your subnets and in the default security group for your worker nodes, you might inadvertently block the subnets and ports that are required for necessary traffic to reach your cluster.
{: tip}

Review the following advantages of security groups over ACLs:
- As opposed to ACLs, security group rules are stateful. When you create a rule to allow traffic in one direction, reverse traffic in response to allowed traffic is automatically permitted without the need for another rule. Fewer rules are required to set up your security group than to set up an ACL.
- An ACL must be created for each subnet that your cluster is attached to, but only one security group must be modified for all worker nodes in your cluster.
- ACLs are applied at the level of the VPC subnet. If one cluster uses multiple subnets, rules are required to ensure that the subnets can communicate with each other. If you create multiple clusters that use the same subnets in one VPC, you can't use ACLs to control traffic between the clusters because they share the same subnets.
- With an ACL, you must explicitly allow traffic in both directions for a connection to succeed.

Regardless of which security option you choose, be sure to follow the instructions for [security groups](#security_groups) or [ACLs](#acls) to allow the subnets and ports that are required for necessary traffic to reach your cluster.

To simplify your VPC security setup, configure inbound and outbound rules either only at the security group level or only at the ACL level. If you configure rules in both ACLs for your subnets and in the default security group for your worker nodes, you might inadvertently block the subnets and ports that are required for necessary traffic to reach your cluster.
{: tip}



## Controlling traffic with the default security group
{: #security_groups}
{: help}
{: support}

Control inbound and outbound traffic to your worker nodes by modifying a VPC security group.
{: shortdesc}

**Level of application**: Worker node

**Default behavior**: VPC security groups are applied to the network interface of a single virtual server to filter traffic at the hypervisor level. Security group rules are not applied in a particular order. However, requests to your worker nodes are only permitted if the request matches one of the rules that you specify. When you allow traffic in one direction by creating an inbound or outbound rule, responses are also permitted in the opposite direction. Security groups are additive, meaning that if your worker nodes are attached to more than one security group, all rules included in the security groups are applied to the worker nodes.

The default rules of the security group for your cluster differs with your cluster's version.
* {{site.data.keyword.openshiftshort}} version 4.5 or later:
    * The default security group for the VPC is applied to your worker nodes. This security group allows incoming ICMP packets (pings) and incoming traffic from other worker nodes in your cluster.
    * Additionally, a unique security group that is named in the format `kube-<cluster_ID>` is automatically created and applied to the worker nodes for that cluster. This security group allows incoming traffic requests to the 30000 - 32767 port range on your worker nodes, and ensures that all inbound and outbound traffic to the pod subnet is permitted so that worker nodes can communicate with each other across subnets.
* {{site.data.keyword.openshiftshort}} version 4.4 or earlier: The default security group for the VPC is applied to your worker nodes. This security group denies all incoming traffic requests to your worker nodes.

**Use case**: Add inbound and outbound rules to a security group to manage the inbound and outbound traffic to your VPC cluster. The way that you modify the security group differs with your cluster version.
* {{site.data.keyword.openshiftshort}} version 4.5 or later:
    * Modify the default security group that is applied to the entire VPC (not unique to your cluster).
    * Do **not** modify or delete the unique `kube-<cluster_ID>` security group that is automatically created for the cluster.
* {{site.data.keyword.openshiftshort}} version 4.4 or earlier: Modify the default security group that is applied to the entire VPC (not unique to your cluster). You **must** modify the default security group to allow inbound traffic to the `30000 - 32767` node port range to allow any incoming requests to apps that run on your worker nodes.

**Limitations**: Because the worker nodes of your VPC cluster exist in a service account and are not listed in the VPC infrastructure dashboard, you can't create a security group and apply it to your worker node instances. You can only modify the existing security group that is created for you.

For more information, see the [VPC documentation](/docs/vpc?topic=vpc-using-security-groups){: external}.

### Creating security group rules from the console
{: #security_groups_ui}

Use the {{site.data.keyword.cloud_notm}} console to add inbound and outbound rules to the default security group for your cluster.
{: shortdesc}

1. From the [Virtual private cloud dashboard](https://cloud.ibm.com/vpc-ext/network/vpcs){: external}, click the name of the **Default Security Group** for the VPC that your cluster is in.
2. Click the **Rules** tab.
3. {{site.data.keyword.openshiftshort}} version 4.4 or earlier only: Add a rule to allow incoming traffic requests through the `30000 - 32767` node port range on your worker nodes.
    1. In the **Inbound rules** section, click **Create**.
    2. Choose the **TCP** protocol, enter `30000` for the **Port min** and `32767` for the **Port max**, and leave the **Any** source enter selected.
    3. Click **Save**.
    4. If you require VPC VPN access or classic infrastructure access into this cluster, repeat these steps to add a rule that uses the **UDP** protocol, `30000` for the **Port min**, `32767` for the **Port max**, and the **Any** source type.
4. To create new rules to control inbound traffic to your worker nodes, in the **Inbound rules** section, click **Create**. Keep in mind that in addition to any rules that you create, the rules in the following table are required to allow necessary inbound traffic to your cluster.
    | Rule purpose | Protocol | Port or Value | Type |
    | --- | --- | --- | --- |
    | Allow all worker nodes in this cluster to communicate with each other. | ALL | - | Security group `<SG_name>` |
    | Allow incoming ICMP packets (pings). | ICMP | Type `8` | Any |
    | {{site.data.keyword.openshiftshort}} version < 4.5: Allow incoming traffic requests to apps that run on your worker nodes. | TCP | `30000` - `32767` | Any |
    | {{site.data.keyword.openshiftshort}} version < 4.5: If you require VPC VPN access or classic infrastructure access into this cluster, allow incoming traffic requests to apps that run on your worker nodes. | UDP | `30000` - `32767` | Any |
    | `*` For Classic clusters, allow access from the {{site.data.keyword.openshiftshort}} control plane IP addresses that are used to health check and report the overall status of your Ingress components. Create one rule for each [control plane CIDR for the region where your cluster is located](https://github.com/IBM-Cloud/kube-samples/tree/master/control-plane-ips){: external}. For VPC clusters, if you use your own security group to the LBaaS for Ingress, set port 80 to allow access from the {{site.data.keyword.openshiftshort}} control plane IP addresses. | TCP | `80` | Each [control plane CIDR for the region where your cluster is located](https://github.com/IBM-Cloud/kube-samples/tree/master/control-plane-ips){: external}. |
    {: caption="Table 2. Required inbound rules" caption-side="top"}
    {: summary="The table shows required inbound connectivity rules for your VPC security group. Rows are read from the left to right, with the purpose of the rule in column one, the protocol in column two, the required ports or values for the protocol in column in three, and the source type and a brief description of the service in column two."}

    `*` Alternatively, to allow the inbound traffic for router health checks, you can create a single rule to allow all incoming traffic on port 80.
5. To create new rules to control outbound traffic to your worker nodes, in the **Outbound rules** section, delete the default rule that allows all outbound traffic.
6. In the **Outbound rules** section, click **Create**. Keep in mind that in addition to any rules that you create, the rules in the following table are required to allow necessary outbound traffic from your cluster.
    | Rule purpose | Protocol | Port or Value | Source type |
    | --- | --- | --- | --- |
    | Allow worker nodes to be created in your cluster. | ALL | - | CIDR block `161.26.0.0/16` |
    | Allow worker nodes to communicate with other {{site.data.keyword.cloud_notm}} services that support private cloud service endpoints, and in clusters that run {{site.data.keyword.openshiftshort}} version 4.5 or earlier, with the cluster master through the private cloud service endpoint. | ALL | - | CIDR block `166.8.0.0/14` |
    | Allow all worker nodes in this cluster to communicate with each other. | ALL | - | Security group `<SG_name>` |
    | Allow outbound traffic to be sent to the Virtual private endpoint gateway which is used to talk to the Kubernetes master. | ALL | - | Virtual private endpoint gateway IP addresses. The Virtual private endpoint gateway is assigned an IP address from a VPC subnet in each of the zones where your cluster has a worker node. For example, if the cluster spans 3 zones, there will be up to 3 IP addresses assigned to each Virtual private endpoint gateway. To find the Virtual private endpoint gateway IPs:  \n 1. Go to the [Virtual private cloud dashboard](https://cloud.ibm.com/vpc-ext/network/vpcs){: external}.  \n 2. Click **Virtual private endpoint gateways**, then select the **Region** where you cluster is located.  \n 3. Find your cluster, then click the IP addresses in the **IP Address** column to copy them. |
    {: caption="Table 2. Required outbound rules" caption-side="top"}
    {: summary="The table shows required outbound connectivity rules for your VPC security group. Rows are read from the left to right, with the purpose of the rule in column one, the protocol in column two, the required ports or values for the protocol in column in three, and the source type and a brief description of the service in column two."}



### Creating security group rules with the CLI
{: #security_groups_cli}

Use the {{site.data.keyword.cloud_notm}} CLI to add inbound and outbound rules to the default security group for your cluster.
{: shortdesc}

Before you begin
1. Install the `infrastructure-service` plug-in. The prefix for running commands is `ibmcloud is`.
    ```sh
    ibmcloud plugin install infrastructure-service
    ```
    {: pre}

2. Target the region that your VPC is in.
    ```sh
    ibmcloud target -r <region>
    ```
    {: pre}

3. Get your cluster's **ID**.
    ```sh
    ibmcloud oc cluster get -c <cluster_name>
    ```
    {: pre}

To create rules in your default security group:

1. List your security groups and note the **ID** of the default security group for your **VPC**. Note that the default security group uses a randomly generated name, and does **not** use the name in the format `kube-<cluster_ID>`.
    ```sh
    ibmcloud is sgs
    ```
    {: pre}

    Example output with the default security group for the VPC of a randomly generated name, `chamomile-dislodge-showier-unfilled`:
    ```sh
    ID                                          Name                                       Rules   Network interfaces   VPC          Resource group
    1a111a1a-a111-11a1-a111-111111111111        chamomile-dislodge-showier-unfilled        5       2                    events-vpc   default
    2b222b2b-b222-22b2-b222-222222222222        kube-df253b6025d64744ab99ed63bb4567b6      5       3                    gen2-vpn     default
    ```
    {: screen}

2. Store the security group ID as an environment variable.
    ```sh
    sg=<security_group_ID>
    ```
    {: pre}

3. Optional: Check out the default rules for the security group.
    ```sh
    ibmcloud is sg $sg
    ```
    {: pre}

4. {{site.data.keyword.openshiftshort}} version 4.4 or earlier only: Allow incoming traffic requests through the `30000 - 32767` node port range.
    1. Add a rule to allow inbound TCP traffic on ports 30000-32767.
        ```sh
        ibmcloud is security-group-rule-add $sg inbound tcp --port-min 30000 --port-max 32767
        ```
        {: pre}

    2. If you require VPC VPN access or classic infrastructure access into this cluster, add a rule to allow inbound UDP traffic on ports 30000-32767.
        ```sh
        ibmcloud is security-group-rule-add $sg inbound udp --port-min 30000 --port-max 32767
        ```
        {: pre}

5. To create new rules to control inbound traffic to your worker nodes, use the [`ibmcloud is security-group-rule-add` command](/docs/vpc?topic=vpc-infrastructure-cli-plugin-vpc-reference#security-group-rule-add).
    ```sh
    ibmcloud is security-group-rule-add $sg inbound <protocol> [--remote <remote_address> | <CIDR_block> | <security_group_ID>] [--icmp-type <icmp_type> [--icmp-code <icmp_code>]] [--port-min <port_min>] [--port-max <port_max>]
    ```
    {: pre}

    Keep in mind that in addition to any rules that you create, the rules in the following table are required to allow necessary inbound traffic to your cluster.
    
    | Rule purpose | Protocol | Port or Value | Source type |
    | --- | --- | --- | --- |
    | Allow all worker nodes in this cluster to communicate with each other. | ALL | - | Security group `kube-<cluster_ID>` |
    | Allow incoming ICMP packets (pings). | ICMP | Type `B` | Any |
    | {{site.data.keyword.openshiftshort}} version < 4.5: Allow incoming traffic requests to apps that run on your worker nodes. | TCP | `3000` - `32767` | Any |
    | {{site.data.keyword.openshiftshort}} version < 4.5: If you require VPC VPN access or classic infrastructure access into this cluster, allow incoming traffic requests to apps that run on your worker nodes. | UDP | `3000` - `32767` | Any |
    | `*` Allow access from the {{site.data.keyword.openshiftshort}} control plane IP addresses that are used to health check and report the overall status of your Ingress components. Create one rule for each [control plane CIDR for the region where your cluster is located](https://github.com/IBM-Cloud/kube-samples/tree/master/control-plane-ips){: external}. | TCP | `80` | Each [control plane CIDR for the region where your cluster is located](https://github.com/IBM-Cloud/kube-samples/tree/master/control-plane-ips){: external}. |
    {: caption="Table 3. Required inbound rules" caption-side="top"}
    {: summary="The table shows required inbound connectivity rules for your VPC security group. Rows are read from the left to right, with the purpose of the rule in column one, the protocol in column two, the required ports or values for the protocol in column in three, and the source type and a brief description of the service in column two."}
    
    `*` Alternatively, to allow the inbound traffic for router health checks, you can create a single rule to allow all incoming traffic on port 80.

6. To create new rules to control outbound traffic to your worker nodes, get the ID of the default rule that allows all outbound traffic.
    ```sh
    ibmcloud is sg $sg
    ```
    {: pre}

    In this example output, the outbound rule that allows all outbound traffic to all destinations (`0.0.0.0/0`) is `r010-93ae3092-cce1-4b89-894c-204e628cf8f3`.
    ```sh
    ...
    Rules
    ID                                          Direction   IP version   Protocol                        Remote
    r010-93ae3092-cce1-4b89-894c-204e628cf8f3   outbound    ipv4         all                             0.0.0.0/0
    r010-e3a34cbb-d5e8-4713-a57e-3e35a7458272   inbound     ipv4         all                             freeload-flavored-surging-repaying
    r010-036c3a13-1c16-4425-9667-a4ec34b1702b   inbound     ipv4         icmp Type=8                     0.0.0.0/0
    r010-15591636-6976-493f-a94f-70721702860a   inbound     ipv4         tcp Ports:Min=22,Max=22         0.0.0.0/0
    r010-5547cb84-4829-475c-8bdf-be1a39d7936d   inbound     ipv4         tcp Ports:Min=30000,Max=32767   0.0.0.0/0
    ...
    ```
    {: screen}

7. Delete the default rule that allows all outbound traffic.
    ```sh
    ibmcloud is security-group-rule-delete $sg <rule_ID>
    ```
    {: pre}

8. Create new rules to control outbound traffic from your worker nodes.
    ```sh
    ibmcloud is security-group-rule-add $sg outbound <protocol> [--remote <remote_address> | <CIDR_block> | <security_group_ID>] [--icmp-type <icmp_type> [--icmp-code <icmp_code>]] [--port-min <port_min>] [--port-max <port_max>]
    ```
    {: pre}

    Keep in mind that in addition to any rules that you create, the rules in the following table are required to allow necessary outbound traffic from your cluster.
    
    | Rule purpose | Protocol | Port or Value | Source type |
    | --- | --- | --- | --- |
    | Allow worker nodes to be created in your cluster. | ALL | - | CIDR block `161.26.0.0/16` |
    | Allow worker nodes to communicate with other {{site.data.keyword.cloud_notm}} services that support private cloud service endpoints, and in clusters that run {{site.data.keyword.openshiftshort}} version 4.5 or earlier, with the cluster master through the private cloud service endpoint. | ALL | - | CIDR block `166.8.0.0/14` |
    | Allow all worker nodes in this cluster to communicate with each other. | ALL | - | Security group `kube-<cluster_ID>` |
    | Allow outbound traffic to be sent to the Virtual private endpoint gateway which is used to talk to the Kubernetes master. | ALL | - | Virtual private endpoint gateway IP addresses. The Virtual private endpoint gateway is assigned an IP address from a VPC subnet in each of the zones where your cluster has a worker node. For example, if the cluster spans 3 zones, there will be up to 3 IP addresses assigned to each Virtual private endpoint gateway. To find the Virtual private endpoint gateway IPs:  \n 1. Go to the [Virtual private cloud dashboard](https://cloud.ibm.com/vpc-ext/network/vpcs){: external}.  \n 2. Click **Virtual private endpoint gateways**, then select the **Region** where you cluster is located.  \n 3. Find your cluster, then click the IP addresses in the **IP Address** column to copy them. |
    {: caption="Table 4. Required outbound rules" caption-side="top"}
    {: summary="The table shows required outbound connectivity rules for your VPC security group. Rows are read from the left to right, with the purpose of the rule in column one, the protocol in column two, the required ports or values for the protocol in column in three, and the source type and a brief description of the service in column two."}

9. Verify that your security group rules are created and that all required rules exist in your security group.
    ```sh
    ibmcloud is sg $sg
    ```
    {: pre}

To simplify your VPC security setup, leave your default ACL for the VPC as-is. If you configure rules in both ACLs for your subnets and in the default security group for your worker nodes, you might inadvertently block the subnets and ports that are required for necessary traffic to reach your cluster.
{: tip}


## Controlling traffic with ACLs
{: #acls}

Control inbound and outbound traffic to your cluster by creating and applying access control lists (ACLs) to each subnet that your cluster is attached to. Note that these steps outline the minimum ACL rules that are required for basic cluster functionality. You might need to create additional ACL rules based on your use case.
{: shortdesc}

Looking for a simpler security setup? Leave the default ACL for your VPC as-is, and modify the [default security group](#security_groups) instead.
{: tip}

**Level of application**: VPC subnet

**Default behavior**: When you create a VPC, a default ACL is created in the format `allow-all-network-acl-<VPC_ID>` for the VPC. The ACL includes an inbound rule and an outbound rule that allow all traffic to and from your subnets. Any subnet that you create in the VPC is attached to this ACL by default. ACL rules are applied in a particular order. When you allow traffic in one direction by creating an inbound or outbound rule, you must also create a rule for responses in the opposite direction because responses are not automatically permitted.

**Use case**: If you want to specify which traffic is permitted to the worker nodes on your VPC subnets, you can create a custom ACL for each subnet in the VPC. For example, you can create the following set of ACL rules to block most inbound and outbound network traffic of a cluster, while allowing communication that is necessary for the cluster to function.

**Limitations**: If you create multiple clusters that use the same subnets in one VPC, you can't use ACLs to control traffic between the clusters because they share the same subnets. You can use [Calico network policies](/docs/openshift?topic=openshift-network_policies#isolate_workers) to isolate your clusters on the private network.

When you use the following steps to create custom ACLs, only network traffic that is specified in the ACL rules is permitted to and from your VPC subnets. All other traffic that is not specified in the ACLs is blocked for the subnets, such as cluster integrations with third party services. If you must allow other traffic to or from your worker nodes, be sure to specify those rules where noted in the following steps.
{: important}

For more information, see the [VPC documentation](/docs/vpc?topic=vpc-using-acls){: external}.

### Creating ACLs from the console
{: #acls_ui}

For each subnet that your cluster is attached to, use the {{site.data.keyword.cloud_notm}} VPC console to create a custom ACL with rules that limit inbound and outbound network traffic to only communication that is necessary for the cluster to function. 
{: shortdesc}

Looking for a simpler security setup? Leave the default ACL for your VPC as-is, and modify the [default security group](#security_groups) instead.
{: tip}

1. Multizone clusters only: In the [Subnets for VPC dashboard](https://cloud.ibm.com/vpc-ext/network/subnets){: external}, note the **IP Range** of each subnet that your cluster is attached to.
2. In the [Access control lists for VPC dashboard](https://cloud.ibm.com/vpc-ext/network/acl){: external}, click **New access control list**.
3. Give your ACL a name and choose the VPC and resource group that your subnets are in.
4. In the **Rules** section, delete the default inbound rule and outbound rule that allow all inbound and outbound traffic.
5. In the **Inbound rules** section, create the following rules by clicking **Create**.

    ACL rules are applied to traffic in a specific order. If you must create custom rules to allow other traffic to or from your worker nodes on this subnet, be sure to set the custom rules' **Priority** before the final rule that denies all traffic. If you add a rule after the deny rule, your rule is ignored, because the packet matches the deny rule and is blocked and removed before it can reach your rule. Note that these steps outline the minimum ACL rules that are required for basic cluster functionality. You might need to create additional ACL rules based on your use case.
    {: note}
    
    | Rule purpose | Allow/Deny | Protocol | Source IP or CIDR | Source Port | Destination IP or CIDR | Destination Port | Priority |
    | --- | --- | --- | --- | --- | --- | --- | -- |
    | Allow worker nodes to be created in your cluster.  | Allow | ALL | `161.26.0.0/16` | - | Any | - | Set to top |
    | Allow worker nodes to communicate with other {{site.data.keyword.cloud_notm}} services that support private cloud service endpoints, and in clusters that run {{site.data.keyword.openshiftshort}} version 4.5 or earlier, with the cluster master through the private cloud service endpoint.  | Allow | ALL | `166.8.0.0/14` | - | Any | - | After 1 |
    | Multizone clusters: Allow worker nodes in one subnet to communicate with the worker nodes in other subnets within the cluster. Create one rule for each subnet that you want to connect to.  | Allow | ALL | Other subnet's CIDR | - | Any | - | After 2 |
    | Allow incoming traffic requests to apps that run on your worker nodes.  | Allow | TCP | Any | Any | Any | `30000 - 32767` | After 3 |
    | To expose apps by using load balancers or Ingress, allow traffic through VPC load balancers. For example, for Ingress listening on `TCP/443`)  | Allow | TCP | Any | Any | Any | 443 | After 4 |
    | `**` For clusters with public and private service endpoints, allow {{site.data.keyword.openshiftshort}} Console pods to contact the master | Allow |  ALL |  Master IPs | - | Any | - | After 5 |
    | `*` Allow access from the {{site.data.keyword.openshiftshort}} control plane IP addresses that are used to health check and report the overall status of your Ingress components. Create one rule for each [control plane CIDR for the region where your cluster is located](https://github.com/IBM-Cloud/kube-samples/tree/master/control-plane-ips){: external}  | Allow | TCP | Each [control plane CIDR for the region where your cluster is located](https://github.com/IBM-Cloud/kube-samples/tree/master/control-plane-ips){: external} | - | Any | `80` | After 6 |
    | Deny all other traffic that does not match the previous rules.  | Deny | ALL | Any | - | Any | - | Set to bottom |
    {: caption="Table 4. Required inbound rules" caption-side="top"}

    `**` Master IPs can be found by looking at the `server:` entry in the cluster's `kubeconfig` file (`kubectl config view`) and then running the *`nslookup`* or *`dig`* command to determine which IPs that it resolves to. The Master IP can be from 1 to 3 different IPs depending on the region and the control plane cluster.
    
    `*` Alternatively, to allow the inbound traffic for router health checks, you can create a single inbound rule and outbound rule to allow all incoming and outgoing traffic on port 80.
    
6. In the **Outbound rules** section, create the following rules by clicking **Create**.

    ACL rules are applied to traffic in a specific order. If you must create custom rules to allow other traffic to or from your worker nodes on this subnet, be sure to set the custom rules' **Priority** before the final rule that denies all traffic. If you add a rule after the deny rule, your rule is ignored, because the packet matches the deny rule and is blocked and removed before it can reach your rule. Note that these steps outline the minimum ACL rules that are required for basic cluster functionality. You might need to create additional ACL rules based on your use case.
   {: note}
   
    | Rule purpose | Allow/Deny | Protocol | Source IP or CIDR | Source Port | Destination IP or CIDR | Destination Port | Priority |
    | --- | --- | --- | --- | --- | --- | --- | -- |
    | Allow worker nodes to be created in your cluster. | Allow | ALL | Any | - | `161.26.0.0/16` | - | Set to top |
    | Allow worker nodes to communicate with other {{site.data.keyword.cloud_notm}} services that support private cloud service endpoints, and in clusters that run {{site.data.keyword.openshiftshort}} version 4.5 or earlier, with the cluster master through the private cloud service endpoint. | Allow | ALL | Any | - | `166.8.0.0/14` | - | After 1 |
    | Multizone clusters: Allow worker nodes in one subnet to communicate with the worker nodes in all other subnets within the cluster. Create one rule for each subnet that you want to connect to.  | Allow | ALL | Any | - | Other subnet's CIDR | - | After 2 |
    | Allow incoming traffic requests to apps that run on your worker nodes. | Allow | TCP | Any | `30000 - 32767` | Any | Any | After 3 |
    | To expose apps by using load balancers or Ingress, allow traffic through VPC load balancers.  | Allow | TCP | Any | `443` | Any | Any | After 4 |
    | `**` For clusters with public and private service endpoints, allow {{site.data.keyword.openshiftshort}} Console pods to contact the master | Allow |  ALL |  Master IPs | - | Any | - | After 5 |
    | `*` Allow access from the {{site.data.keyword.openshiftshort}} control plane IP addresses that are used to health check and report the overall status of your Ingress components. Create one rule for each [control plane CIDR for the region where your cluster is located](https://github.com/IBM-Cloud/kube-samples/tree/master/control-plane-ips){: external}. | Allow | TCP | Any | `80` | Each [control plane CIDR for the region where your cluster is located](https://github.com/IBM-Cloud/kube-samples/tree/master/control-plane-ips){: external}. | Any | After 6 |
    | Deny all other traffic that does not match the previous rules.  | Deny | ALL | Any | - | Any | - | Set to bottom |
    {: caption="Table 6. Required outbound rules" caption-side="top"}

    `**` Master IPs can be found by looking at the `server:` entry in the cluster's `kubeconfig` file (`kubectl config view`) and then running the *`nslookup`* or *`dig`* command to determine which IPs that it resolves to. The Master IP can be from 1 to 3 different IPs depending on the region and the control plane cluster.
    
    `*` Alternatively, to allow the inbound traffic for router health checks, you can create a single inbound rule and outbound rule to allow all incoming and outgoing traffic on port 80.
    
7. In the **Attach subnets** section, choose the name of the subnet for which you created this ACL.

8. Click **Create access control list**.

9. Multizone clusters: Repeat steps 2 - 8 to create an ACL for each subnet that your cluster is attached to.

### Creating ACLs with the CLI
{: #acls_cli}

For each subnet that your cluster is attached to, use the {{site.data.keyword.cloud_notm}} CLI to create a custom ACL with rules that limit inbound and outbound network traffic to only communication that is necessary for the cluster to function. Note that these steps outline the minimum ACL rules that are required to allow a cluster to deploy and to have basic function; they aren't intended to cover all use cases.
{: shortdesc}

Looking for a simpler security setup? Leave the default ACL for your VPC as-is, and modify the [default security group](#security_groups) instead.
{: tip}

Before you begin

1. Install the `infrastructure-service` plug-in. The prefix for running commands is `ibmcloud is`.
    ```sh
    ibmcloud plugin install infrastructure-service
    ```
    {: pre}

2. Target the region that your VPC is in.
    ```sh
    ibmcloud target -r <region>
    ```
    {: pre}

To create an ACL for each subnet that your cluster is attached to,

1. List your VPC subnets. For each subnet that your cluster is attached to, get the **ID** and **Subnet CIDR**.

    If you can't remember which subnets your cluster is attached to, you can run `ibmcloud oc worker get -c <cluster_name_or_ID> -w <worker_node_ID>` for one worker node in each zone of your cluster, and get the **ID** and **CIDR** of the subnet that the worker is attached to.
    {: tip}

    ```sh
    ibmcloud is subnets
    ```
    {: pre}

    Example output

    ```sh
    ID                                          Name          Status      Subnet CIDR        Addresses   ACL                                                  Public Gateway                            VPC       Zone         Resource group
    0717-2224d664-d435-425e-b5ec-f324af2df445   mysubnet1     available   10.240.0.0/28      11/16       armored-never-chitchat-gangly-skylight-prototype     -                                  myvpc     us-south-1   default
    0717-1eff410a-a47e-4bc2-b4a3-5f742f320008   mysubnet2     available   10.240.1.0/24      251/256     armored-never-chitchat-gangly-skylight-prototype     pgw-ed8f6970-9b71-11ea-b94a-956de1af1ccd        myvpc     us-south-2   default
    ```
    {: screen}

2. Create an ACL. After you create the ACL, you can add rules to your ACL and apply the ACL to one subnet. Because the rules that you add to your ACL are specific to one subnet, consider naming the ACL in the format `<cluster>-<subnet>-acl`, such as `mycluster-mysubnet1-acl`, for easy identification. When you create the ACL, two rules are automatically created that allow all inbound and all outbound network traffic. In the output, note the ACL ID and the IDs of the two default rules.
    ```sh
    ibmcloud is network-acl-create <cluster>-<subnet>-acl
    ```
    {: pre}

    Example output

    ```sh
    Creating network ACL mycluster-mysubnet1-acl under account Account as user user@email.com...

    ID        740b07cb-4e69-4ef2-b667-42ed27d8b29e
    Name      mycluster-mysubnet1-acl
    Created   2019-09-18T15:09:45-05:00

    Rules

    inbound
    ID                                     Name                                                          Action   IPv*   Protocol   Source      Destination   Created
    e3caad9c-68b7-4a4a-8188-d239fbc724df   allow-all-inbound-rule-740b07cb-4e69-4ef2-b667-42ed27d8b29e   allow    ipv4   all        0.0.0.0/0   0.0.0.0/0     2019-09-18T15:09:45-05:00

    outbound
    ID                                     Name                                                           Action   IPv*   Protocol   Source      Destination   Created
    7043ac95-cc4e-42e9-a490-22177237f083   allow-all-outbound-rule-740b07cb-4e69-4ef2-b667-42ed27d8b29e   allow    ipv4   all        0.0.0.0/0   0.0.0.0/0     2019-09-18T15:09:45-05:00
    ```
    {: screen}

3. Export the ACL ID as an environment variable.
    ```sh
    export ACL_ID=<acl_id>
    ```
    {: pre}

4. Delete the default rules that allow all inbound and outbound traffic. After, your ACL still exists, but does not contain any networking rules.
    ```sh
    ibmcloud is network-acl-rule-delete $acl_id <default_inbound_rule_ID> -f
    ```
    {: pre}

    ```sh
    ibmcloud is network-acl-rule-delete $acl_id <default_outbound_rule_ID> -f
    ```
    {: pre}

5. Multizone clusters: Add rules to your ACL to allow worker nodes in one subnet to communicate with the worker nodes in all other subnets within the cluster. The subnet for which you create the ACL rule is defined as `0.0.0.0/0` and you use the CIDRs of the other subnets as your destination CIDR. Make sure to create one inbound and one outbound rule for each of the subnets that you want to connect to.
    ```sh
    ibmcloud is network-acl-rule-add $acl_id allow outbound all 0.0.0.0/0 <other_zone_subnet_CIDR> --name allow-workers-outbound
    ```
    {: pre}

    ```sh
    ibmcloud is network-acl-rule-add $acl_id allow inbound all <other_zone_subnet_CIDR> 0.0.0.0/0 --name allow-workers-inbound
    ```
    {: pre}

6. Create rules to allow inbound traffic from and outbound traffic to the `161.26.0.0/16` and `166.8.0.0/14` {{site.data.keyword.cloud_notm}} private subnets. The `161.26.0.0/16` rules allow you to create worker nodes in your cluster. The `166.8.0.0/14` rules allow worker nodes to communicate with other {{site.data.keyword.cloud_notm}} services that support private cloud service endpoints, and in clusters that run {{site.data.keyword.openshiftshort}} version 4.5 or earlier, with the cluster master through the private cloud service endpoint.

    Need to connect your worker nodes to {{site.data.keyword.cloud_notm}} services that support only public cloud service endpoints? [Attach a public gateway to the subnet ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/kubernetes/clusters) so that worker nodes can connect to a public endpoint outside of your cluster. Then, create inbound and outbound rules to allow ingress from and egress to the services' public cloud service endpoints.
    {: tip}

    ```sh
    ibmcloud is network-acl-rule-add $acl_id allow outbound all 0.0.0.0/0 161.26.0.0/16 --name allow-ibm-private-network-outbound1
    ibmcloud is network-acl-rule-add $acl_id allow outbound all 0.0.0.0/0 166.8.0.0/14 --name allow-ibm-private-network-outbound2
    ibmcloud is network-acl-rule-add $acl_id allow inbound all 161.26.0.0/16 0.0.0.0/0 --name allow-ibm-private-network-inbound1
    ibmcloud is network-acl-rule-add $acl_id allow inbound all 166.8.0.0/14 0.0.0.0/0 --name allow-ibm-private-network-inbound2
    ```
    {: pre}

7. To allow incoming traffic requests to apps that run on your worker nodes through router services or load balancers, allow traffic to the VPC load balancer on port `443` and to worker nodes on ports `30000 - 32767`.
    ```sh
    ibmcloud is network-acl-rule-add $acl_id allow outbound tcp 0.0.0.0/0 0.0.0.0/0 --name allow-lb-outbound --source-port-min 443 --source-port-max 443
    ibmcloud is network-acl-rule-add $acl_id allow inbound tcp 0.0.0.0/0 0.0.0.0/0 --name allow-lb-inbound --destination-port-min 443 --destination-port-max 443
    ibmcloud is network-acl-rule-add $acl_id allow outbound tcp 0.0.0.0/0 0.0.0.0/0 --name allow-ingress-outbound --source-port-min 30000 --source-port-max 32767
    ibmcloud is network-acl-rule-add $acl_id allow inbound tcp 0.0.0.0/0 0.0.0.0/0 --name allow-ingress-inbound --destination-port-min 30000 --destination-port-max 32767  
    ```
    {: pre}

8. Optional: Allow access to and from the {{site.data.keyword.openshiftshort}} control plane IP addresses that are used to health check and report the overall status of your Ingress components. Create one inbound and one outbound rule for each [control plane CIDR for the region where your cluster is located](https://github.com/IBM-Cloud/kube-samples/tree/master/control-plane-ips){: external}. Alternatively, you can create a single inbound rule and outbound rule to allow all incoming and outgoing traffic on port 80.
    ```sh
    ibmcloud is network-acl-rule-add $acl_id allow outbound tcp 0.0.0.0/0 <IP_address> --name allow-hc-outbound --source-port-min 80 --source-port-max 80
    ibmcloud is network-acl-rule-add $acl_id allow inbound tcp <IP_address> 0.0.0.0/0 --name allow-hc-inbound --destination-port-min 80 --destination-port-max 80
    ```
    {: pre}

9. Optional: If you must allow other traffic to or from your worker nodes on this subnet, add rules for that traffic.

    When you refer to the VPC subnet that your worker nodes are on, you must use `0.0.0.0/0`. For more tips on how to create your rule, see the [VPC CLI reference documentation](/docs/vpc?topic=vpc-infrastructure-cli-plugin-vpc-reference#network-acl-rule-add).
    {: note}

    ```sh
    ibmcloud is network-acl-rule-add $acl_id <allow|deny> <inbound|outbound> <protocol> <source_CIDR> <destination_CIDR> --name <new_rule_name>
    ```
    {: pre}

    For example, say that you want your worker nodes to communicate with a subnet in your organization's network, `207.42.8.0/24`. Your worker nodes must be able to both send and receive information from devices or services on this subnet. You can create an outbound rule for traffic to and an inbound rule for traffic from your organization's subnet:
    ```sh
    ibmcloud is network-acl-rule-add $acl_id allow outbound all 0.0.0.0/0 207.42.8.0/24 --name corporate-network-outbound
    ibmcloud is network-acl-rule-add $acl_id allow inbound all 207.42.8.0/24 0.0.0.0/0 --name corporate-network-inbound
    ```
    {: screen}

10. Create rules to deny all other egress from and ingress to worker nodes that is not permitted by the previous rules that you created. Because these rules are created last in the chain of rules, they deny an incoming or outgoing connection only if the connection does not match any other rule that is earlier in the rule chain.
    ```sh
    ibmcloud is network-acl-rule-add $acl_id deny outbound all 0.0.0.0/0 0.0.0.0/0 --name deny-all-outbound
    ibmcloud is network-acl-rule-add $acl_id deny inbound all 0.0.0.0/0 0.0.0.0/0 --name deny-all-inbound
    ```
    {: pre}

11. Apply this ACL to the subnet. When you apply this ACL, the rules that you defined are immediately applied to the worker nodes on the subnet.
    ```sh
    ibmcloud is subnet-update <subnet_ID> --network-acl-id $acl_id
    ```
    {: pre}

    Example output

    ```sh
    ID                  a1b2c3d4-f560-471b-b6ce-20067ac93439
    Name                mysubnet1
    IPv*                ipv4
    IPv4 CIDR           10.240.0.0/24
    IPv6 CIDR           -
    Address Available   244
    Address Total       256
    ACL                 mycluster-mysubnet1-acl(b664769d-514c-407f-a9f3-d44d72706121)
    Gateway             pgw-18a3ebb0-b539-11e9-9838-f3f4efa02374(f8b95e43-a408-4dc8-a489-ed649fc4cfec)
    Created             2019-08-02T10:20:17-05:00
    Status              available
    Zone                us-south-1
    VPC                 myvpc(ff537d43-a5a4-4b65-9627-17eddfa5237b)
    ```
    {: screen}

12. Repeat steps 2 - 11 for each subnet that you found in step 1.

ACL rules are applied to traffic in a specific order. If you want to add a rule after you complete these steps, ensure that you add the rule before the `deny-all-inbound` or `deny-all-outbound` rule. If you add a rule after these rules, your rule is ignored, because the packet matches the `deny-all-inbound` and `deny-all-outbound` rules and is blocked and removed before it can reach your rule. Create your rule in the proper order by including the `--before-rule-name deny-all-(inbound|outbound)` flag.
{: note}


## Controlling traffic between pods with Kubernetes policies
{: #kubernetes_policies}

You can use Kubernetes policies to control network traffic between pods in your cluster and to isolate app microservices from each other within a namespace or across namespaces.
{: shortdesc}

**Level of application**: Worker node host endpoint

**Default behavior**: No Kubernetes network policies exist by default in your cluster. By default, any pod has access to any other pod in the cluster. Additionally, any pod has access to any services that are exposed by the pod network, such as a metrics service, the cluster DNS, the API server, or any services that you manually create in your cluster.

**Use case**: Kubernetes network policies specify how pods can communicate with other pods and with external endpoints. Both incoming and outgoing network traffic can be allowed or blocked based on protocol, port, and source or destination IP addresses. Traffic can also be filtered based on pod and namespace labels. When Kubernetes network policies are applied, they are automatically converted into Calico network policies. The Calico network plug-in in your cluster enforces these policies by setting up Linux Iptables rules on the worker nodes. Iptables rules serve as a firewall for the worker node to define the characteristics that the network traffic must meet to be forwarded to the targeted resource.

If most or all pods don't require access to specific pods or services, and you want to ensure that pods by default can't access those pods or services, you can create a Kubernetes network policy to block ingress traffic to those pods or services.

For more information about how Kubernetes network policies control pod-to-pod traffic and for more example policies, see the [Kubernetes documentation](https://kubernetes.io/docs/concepts/services-networking/network-policies/){: external}.
{: tip}

### Isolate app services within a namespace
{: #services_one_ns}

The following scenario demonstrates how to manage traffic between app microservices within one namespace.
{: shortdesc}

An Accounts team deploys multiple app services in one namespace, but they need isolation to permit only necessary communication between the microservices over the public network. For the app `Srv1`, the team has front end, back end, and database services. They label each service with the `app: Srv1` label and the `tier: frontend`, `tier: backend`, or `tier: db` label.

![Use a network policy to manage cross-namespace traffic.](images/cs_network_policy_single_ns.png "Use a network policy to manage cross-namespace traffic"){: caption="Figure 1. Use a network policy to manage cross-namespace traffic" caption-side="bottom"}

The Accounts team wants to allow traffic from the front end to the back end, and from the back end to the database. They use labels in their network policies to designate which traffic flows are permitted between microservices.

First, they create a Kubernetes network policy that allows traffic from the front end to the back end:

```yaml
kind: NetworkPolicy
apiVersion: networking.k8s.io/v1
metadata:
  name: backend-allow
spec:
  podSelector:
    matchLabels:
      app: Srv1
      tier: backend
  ingress:
  - from:
    - podSelector:
        matchLabels:
          app: Srv1
          Tier: frontend
```
{: codeblock}

The `spec.podSelector.matchLabels` section lists the labels for the Srv1 back-end service so that the policy applies only _to_ those pods. The `spec.ingress.from.podSelector.matchLabels` section lists the labels for the Srv1 front-end service so that ingress is permitted only _from_ those pods.

Then, they create a similar Kubernetes network policy that allows traffic from the back end to the database:

```yaml
kind: NetworkPolicy
apiVersion: networking.k8s.io/v1
metadata:
  name: db-allow
spec:
  podSelector:
    matchLabels:
      app: Srv1
      tier: db
  ingress:
  - from:
    - podSelector:
        matchLabels:
          app: Srv1
          Tier: backend
```
{: codeblock}

The `spec.podSelector.matchLabels` section lists the labels for the Srv1 database service so that the policy applies only _to_ those pods. The `spec.ingress.from.podSelector.matchLabels` section lists the labels for the Srv1 back-end service so that ingress is permitted only _from_ those pods.

Traffic can now flow from the front end to the back end, and from the back end to the database. The database can respond to the back end, and the back end can respond to the front end, but no reverse traffic connections can be established.

### Isolate app services between namespaces
{: #services_across_ns}

The following scenario demonstrates how to manage traffic between app microservices across multiple namespaces.
{: shortdesc}

Services that are owned by different subteams need to communicate, but the services are deployed in different namespaces within the same cluster. The Accounts team deploys front end, back end, and database services for the app Srv1 in the accounts namespace. The Finance team deploys front end, back end, and database services for the app Srv2 in the finance namespace. Both teams label each service with the `app: Srv1` or `app: Srv2` label and the `tier: frontend`, `tier: backend`, or `tier: db` label. They also label the namespaces with the `usage: accounts` or `usage: finance` label.

![Use a network policy to manage cross-namepspace traffic.](images/cs_network_policy_multi_ns.png) "Use a network policy to manage cross-namespace traffic"){: caption="Figure 1. Use a network policy to manage cross-namespace traffic" caption-side="bottom"}

The Finance team's Srv2 needs to call information from the Accounts team's Srv1 back end. So the Accounts team creates a Kubernetes network policy that uses labels to allow all traffic from the finance namespace to the Srv1 back end in the accounts namespace. The team also specifies the port 3111 to isolate access through that port only.

```yaml
kind: NetworkPolicy
apiVersion: networking.k8s.io/v1
metadata:
  Namespace: accounts
  name: accounts-allow
spec:
  podSelector:
    matchLabels:
      app: Srv1
      Tier: backend
  ingress:
  - from:
    - NamespaceSelector:
        matchLabels:
          usage: finance
      ports:
        port: 3111
```
{: codeblock}

The `spec.podSelector.matchLabels` section lists the labels for the Srv1 back-end service so that the policy applies only _to_ those pods. The `spec.ingress.from.NamespaceSelector.matchLabels` section lists the label for the finance namespace so that ingress is permitted only _from_ services in that namespace.

Traffic can now flow from finance microservices to the accounts Srv1 back end. The accounts Srv1 back end can respond to finance microservices, but can't establish a reverse traffic connection.

In this example, all traffic from all microservices in the finance namespace is permitted. You can't allow traffic from specific app pods in another namespace because `podSelector` and `namespaceSelector` can't be combined.


