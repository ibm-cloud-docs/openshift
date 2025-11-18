---

copyright: 
  years: 2023, 2025
lastupdated: "2025-11-18"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, firewall, acl, acls, access control list, rules, security group

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}



# Creating and managing VPC security groups
{: #vpc-security-group-manage}
{: help}
{: support}

[Virtual Private Cloud]{: tag-vpc}
[4.15 and later]{: tag-red}



## Adding security groups during cluster creation
{: #vpc-sg-cluster}

When you create a VPC cluster, the default worker security group, which is named `kube-<clusterID>`, is automatically created and applied to all workers in the cluster. You can also attach additional security groups alongside the default worker security group. The security groups applied to the workers in the cluster are a combination of the security groups applied when you create the cluster and when you create the worker pool. A total of five security groups can be applied to your cluster.
{: shortdesc}

The security groups applied to a cluster cannot be changed once the cluster is created. You can change the rules of the security groups that are applied to the cluster, but you cannot add or remove security groups at the cluster level. If you apply the incorrect security groups at cluster create time, you must delete the cluster and create a new one. 
{: important}

### If you only want the default security groups
{: #default-sgs-only}

When you create your cluster, do not specify any additional security groups.

```sh
 ibmcloud oc cluster create vpc-gen2 --name <cluster-name> --zone <zone> --vpc-id <vpc-id> --subnet-id <subnet-id>
```
{: pre}


## Viewing security groups
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

1. List the security groups attached to the VPC that your cluster is in. The VPC security group is assigned a randomly generated name, such as `trench-hexagon-matriarch-flower`. The cluster security group is named in the format of `kube-<cluster-ID>`.

    ```sh
    ibmcloud is sgs | grep <vpc_name>
    ```
    {: pre}

    Example output

    ```sh
    ID                                          Name                                             Rules   Network interfaces   VPC                          Resource group   

    r006-111aa1aa-1a1a-1a11-1111-a111aaa1a11a   trench-hexagon-matriarch-flower                    4       0                    my-vpc                      default   
    r006-222aa2aa-2a2a-2a22-2222-a222aaa2a22a   kube-a111a11a11aa1aa11a11                          4       0                    my-vpc                      default   
    r006-333aa3aa-3a3a-3a33-3333-a333aaa3a33a   kube-r006-111a11aa-aaa1-1a1a-aa11-1a1a111aa11      4       0                    my-vpc                      default   
    ```
    {: screen}

1. Get the details of a security group. Find the **Rules** section in the output to view the inbound and outbound rules attached to the security group.

    ```sh
    ibmcloud is sg GROUP
    ```
    {: pre}

    Example output

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

## Viewing security groups in the console
{: #vpc-sg-ui}
{: ui}

1. From the [Security groups for VPC dashboard](https://cloud.ibm.com/infrastructure/network/securityGroups){: external}, find the security groups that are attached to the VPC that your cluster is in.
1. Click the security group.

    To sort the security groups by the VPC they are attached to, click the **Virtual Private Cloud** column heading in the table. 
    {: tip}

1. To view the inbound and outbound rules attached to the security group, click the **Rules** tab.


## Creating security group rules in the console
{: #security-group-inbound-rules}
{: ui}

1. From the [Virtual private cloud dashboard](https://cloud.ibm.com/infrastructure/network/vpcs){: external}, click the name of the **Default Security Group** for the VPC that your cluster is in.
1. Click the **Rules** tab.
    *  To create new inbound rules to control inbound traffic to your worker nodes, in the **Inbound rules** section, click **Create**. 
    * To create new rules to control outbound traffic to your worker nodes, in the **Outbound rules** section, click **Create**.

	After adding rules, do not delete the default that allows all outbound traffic from the console. Instead, run the `ibmcloud is security-group-rule-delete` command from the CLI to remove the rule.
	{: note}


## Creating security group rules in the command line
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
    ibmcloud target -r REGION
    ```
    {: pre}

1. Get your cluster's **ID**.
    ```sh
    ibmcloud oc cluster get -c CLUSTER
    ```
    {: pre}

1. List your security groups and note the **ID**.
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
    sg=GROUP
    ```
    {: pre}

1. Review the default rules for the security group.
    ```sh
    ibmcloud is sg $sg
    ```
    {: pre}

    * To create inbound traffic rules, use the [`ibmcloud is sg-rulec <sg> inbound` command](/docs/vpc?topic=vpc-creating-vpc-resources-with-cli-and-api&interface=cli#add-rules-to-default-security-group).
        ```sh
        ibmcloud is sg-rulec $sg inbound <protocol> [--remote <remote_address> | <CIDR_block> | <security_group_ID>] [--icmp-type <icmp_type> [--icmp-code <icmp_code>]] [--port-min <port_min>] [--port-max <port_max>]
        ```
        {: pre}
        
        
    * To create outbound traffic rules, use the [`ibmcloud is sg-rulec <sg> outbound` command](/docs/vpc?topic=vpc-creating-vpc-resources-with-cli-and-api&interface=cli#add-rules-to-default-security-group).

        ```sh
        ibmcloud is sg-rulec $sg outbound <protocol> [--remote <remote_address> | <CIDR_block> | <security_group_ID>] [--icmp-type <icmp_type> [--icmp-code <icmp_code>]] [--port-min <port_min>] [--port-max <port_max>]
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
