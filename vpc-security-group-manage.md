---

copyright: 
  years: 2023, 2024
lastupdated: "2024-09-23"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, firewall, acl, acls, access control list, rules, security group

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}



# Creating and managing VPC security groups
{: #vpc-security-group-manage}
{: help}
{: support}

[Virtual Private Cloud]{: tag-vpc}



**4.14** and earlier: If you modify the default VPC security group, you must, at minimum, include the [required rules](/docs/openshift?topic=openshift-vpc-security-group) so that your cluster works properly.
{: note}




## Adding security groups during cluster creation
{: #vpc-sg-cluster}

When you create a VPC cluster, the default worker security group, which is named `kube-<clusterID>`, is automatically created and applied to all workers in the cluster. You can also attach additional security groups alongside the default worker security group. The security groups applied to the workers in the cluster are a combination of the security groups applied when you create the cluster and when you create the worker pool. A total of five security groups can be applied to workers, including the default security groups and any security groups applied to the worker pool. Note that the option to add custom security groups to workers is only available in the CLI. 
{: shortdesc}

The security groups applied to a cluster cannot be changed once the cluster is created. You can change the rules of the security groups that are applied to the cluster, but you cannot add or remove security groups at the cluster level. If you apply the incorrect security groups at cluster create time, you must delete the cluster and create a new one. 
{: important}

### If you only want the default security groups
{: #default-sgs-only}

[VPC security group]{: tag-blue} [Worker security group]{: tag-red}

Note that this is the default behavior at cluster create time.
{: note}

When you create your cluster, do not specify any additional security groups. 

Example command to create a VPC cluster with only the default VPC and `kube-<clusterID>` cluster security groups:

```sh
 ibmcloud oc cluster create vpc-gen2 --name <cluster-name> --zone <zone> --vpc-id <vpc-id> --subnet-id <subnet-id>
```
{: pre}

The following security groups are applied:
- The default VPC security group (randomly generated name)
- The `kube-<clusterID>` worker security group.

 
### If you want the cluster security group and your own additional security groups
{: #cluster-customer-sgs} 

[VPC security group]{: tag-blue} [Worker security group]{: tag-red} [Your own security groups]{: tag-warm-gray}

When you create the cluster, specify `--cluster-security-group cluster` and up to four additional security groups that you own. You must include a separate `--cluster-security-group` option for each individual security group you want to add. Note that at maximum of five security groups can be applied to workers, including the security groups that are applied by default. 

Example command to create a VPC cluster with the `kube-<clusterID>` cluster security group and your own additional security groups:
```sh
 ibmcloud oc cluster create vpc-gen2 --name <cluster-name> --zone <zone> --vpc-id <vpc-id> --subnet-id <subnet-id> --cluster-security-group cluster --cluster-security-group <group-id-1> --cluster-security-group <group-id-2> --cluster-security-group <group-id-3>
```
{: pre}

The following security groups are applied:
- The default VPC security group (randomly generated name).
- `kube-<clusterID>` worker security group
- Up to four of your own additional security groups, for a maximum of five total security groups. 

### If you only want your own security groups 
{: #customer-sgs-only}

[VPC security group]{: tag-blue} [Your own security groups]{: tag-warm-gray}

This option is only available in clusters created at versions 4.14 and earlier. Beginning with 4.15, all clusters get the worker node security group as well.
{: note}

When you create the cluster, specify up to five security groups that you own. You must include a separate `--cluster-security-group` option for each individual security group you want to add. 

Example command to create a VPC cluster with only your own security groups:
```sh
 ibmcloud oc cluster create vpc-gen2 --name <cluster-name> --zone <zone> --vpc-id <vpc-id> --subnet-id <subnet-id> --cluster-security-group <group-id-1> --cluster-security-group <group-id-2> --cluster-security-group <group-id-3>
```
{: pre}

The following security groups are applied:
- The default VPC security group (randomly generated name)
- Up to four of your own additional security groups, for a maximum of five total security groups. 


## Adding security groups to worker pools during creation
{: #vpc-sg-worker-pool}

By default, the security groups applied to a worker pool are the same security groups that are indicated at cluster create time. However, you can specify additional security groups to apply to a worker pool. If you apply additional security groups to the worker pool, then the security group applied to the workers on the cluster is a combination of the [security groups applied at cluster create](#vpc-sg-cluster) and the security groups applied to the worker pool. 

A maximum of five security groups can be applied to a worker, including the security groups applied by default.
{: note} 

The security groups applied to a worker pool cannot be changed once the worker pool is created. You can change the rules of the security groups that are applied to the worker pool, but you cannot add or remove security groups at the worker pool level. If you apply the incorrect security groups at worker pool create time, you must delete the worker pool and create a new one. 
{: important}

### If you do not want to attach additional security groups to the worker pool
{: #no-worker-sgs}

When you create the worker pool, do not specify any additional security groups.

This scenario only applies to versions 4.14 and earlier.
{: note}

Example command to create a worker pool with no security groups applied:
```sh
ibmcloud oc worker-pool create vpc-gen2 --name <worker_pool_name> --cluster <cluster_name_or_ID> --flavor <flavor> --size-per-zone <number_of_workers_per_zone> 
```
{: pre}

Only the security groups applied to the cluster are applied to the workers.

### If you want to attach additional security groups to the worker pool
{: #worker-sgs}

When you create the worker pool specify additional security groups at worker pool create time. You must include a separate `--security-group` option for each individual security group you want to add.

Example command to create a worker pool with your own security groups applied:
```sh
ibmcloud oc worker-pool create vpc-gen2 --name <worker_pool_name> --cluster <cluster_name_or_ID> --flavor <flavor> --size-per-zone <number_of_workers_per_zone> --security-group <group-id-1> --security-group <group-id-2> --security-group <group-id-3>
```
{: pre}

The security groups applied to the workers in the worker pool are a combination of those applied to the cluster that the worker pool is attached to and those applied to the worker pool at create time.


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

1. List the security groups attached to the VPC that your cluster is in. The VPC security group is assigned a randomly generated name, such as `trench-hexagon-matriarch-flower`. The cluster security group is named in the format of `kube-<cluster-ID>`. The VPC security group is named in the format of `kube-<vpc-ID>`. 

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
1. Click on the security group.

    To sort the security groups by the VPC they are attached to, click the **Virtual Private Cloud** column heading in the table. 
    {: tip}

1. To view the inbound and outbound rules attached to the security group, click the **Rules** tab.


## Creating security group rules in the console
{: #security-group-inbound-rules}
{: ui}

1. From the [Virtual private cloud dashboard](https://cloud.ibm.com/infrastructure/network/vpcs){: external}, click the name of the **Default Security Group** for the VPC that your cluster is in.
1. Click the **Rules** tab.
    *  To create new inbound rules to control inbound traffic to your worker nodes, in the **Inbound rules** section, click **Create**. 
    * To create new rules to control outbound traffic to your worker nodes, in the **Outbound rules** section, delete the default rule that allows all outbound traffic. Then, in the **Outbound rules** section, click **Create**. 

Keep in mind that in addition to any rules you create, you must also create the required [inbound and outbound rules](/docs/openshift?topic=openshift-vpc-security-group).
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
    sg=GROUP
    ```
    {: pre}

1. Review the default rules for the security group. Keep in mind that in addition to any rules you create, you must also create the required [inbound and outbound rules](/docs/openshift?topic=openshift-vpc-security-group).
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
    

Keep in mind that you can create your own security groups as well as add or remove rules  addition to any rules you create, you must also create the required [inbound and outbound rules](/docs/openshift?topic=openshift-vpc-security-group).
{: note}



## Allow worker nodes to connect to the public service endpoint IP addresses for the Oauth service
{: #worker-node-public-service-endpoint}

Required for VPC clusters with a public service endpoint. This scenario applies only to versions 4.14 and earlier.
{: note}

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
    
2. Run `dig +short` or `nslookup` to get the IPs associated with the hostname in the URL. For single-campus multizone regions there is only one public IP associated with the hostname. For multizone regions, there are 3. Look up the individual IPs by replacing `e` with 1, 2, and 3.
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

This scenario applies only to versions 4.14 and earlier.
{: note}

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
