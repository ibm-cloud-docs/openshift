<ff-roks311-vpc>---

copyright:
  years: 2014, 2019
lastupdated: "2019-12-03"

keywords: openshift, roks, rhoks, rhos, firewall, acl, acls, access control list, rules, security group

subcollection: openshift

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:preview: .preview} 

# Controlling traffic with VPC ACLs and network policies
{: #vpc-network-policy}

<img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> This ACL information is specific to VPC clusters. For network policy information for classic clusters, see [Controlling traffic with network policies](/docs/openshift?topic=openshift-network_policies).
{: note}

If you have unique security requirements, you can control traffic to and from your cluster with VPC access control lists (ACLs) and traffic between pods in your cluster with Kubernetes network policies. 
{: shortdesc}

<dl>
<dt>[VPC access control lists (ACLs)](/docs/vpc-on-classic-network?topic=vpc-on-classic-network-setting-up-network-acls)</dt>
<dd>VPC ACLs specify rules that are applied at the level of each VPC subnet.<ul><li>By using inbound rules, you can allow or deny traffic from a source IP range with specified protocols and ports. The destination IP range is determined by the subnet that you attach the ACL to.</li><li>By using outbound rules, you can allow or deny traffic to a source IP range with specified protocols and ports. The source IP range is determined by the subnet that you attach the ACL to.</li></ul><p class="note">Although Calico policies are supported in VPC clusters, you can remain VPC-native by using VPC ACLs for your subnets instead. However, if you create multiple clusters that use the same subnets in one VPC, you cannot use ACLs to control traffic between the clusters because they share the same subnets. You can use [Calico network policies](/docs/openshift?topic=openshift-network_policies#isolate_workers) to isolate your clusters on the private network.</p></dd>
<dt>[Kubernetes network policies ![External link icon](../icons/launch-glyph.svg "External link icon")](https://kubernetes.io/docs/concepts/services-networking/network-policies/)</dt>
<dd>Kubernetes network policies specify how pods can communicate with other pods and with external endpoints. As of Kubernetes version 1.8, both incoming and outgoing network traffic can be allowed or blocked based on protocol, port, and source or destination IP addresses. Traffic can also be filtered based on pod and namespace labels. Kubernetes network policies are applied by using `oc` commands or the Kubernetes APIs. When these policies are applied, they are automatically converted into Calico network policies. The Calico network plug-in in your cluster enforces these policies by setting up Linux Iptables rules on the Kubernetes worker nodes. Iptables rules serve as a firewall for the worker node to define the characteristics that the network traffic must meet to be forwarded to the targeted resource.</dd>
</dl>

You cannot use [VPC security groups](/docs/infrastructure/security-groups?topic=security-groups-about-ibm-security-groups#about-ibm-security-groups) to control traffic for your worker nodes. VPC security groups are applied to the network interface of a single virtual server to filter traffic at the hypervisor level. However, the worker nodes of your VPC cluster exist in a service account and are not listed in the VPC infrastructure dashboard. You cannot attach a security group to your worker nodes instances.
{: note}

<br />


## Restricting public network traffic to a subnet with a public gateway
{: #vpc-gateway}

Improve the security of your {{site.data.keyword.openshiftlong}} cluster by allowing fewer worker nodes to have external access through a VPC subnet public gateway.
{:shortdesc}

If pods on your worker nodes need to connect to a public external endpoint, you can attach a [public gateway](/docs/vpc-on-classic-network?topic=vpc-on-classic-network-about-networking-for-vpc#use-a-public-gateway) to the subnet that those worker nodes are on. For example, your VPC cluster can automatically connect to other [{{site.data.keyword.cloud_notm}} services that support private service endpoints](/docs/resources?topic=resources-private-network-endpoints), such as {{site.data.keyword.registrylong_notm}}. However, if you need to access {{site.data.keyword.cloud_notm}} services that support only public service endpoints, you can attach a public gateway to the subnet so that your pods can send requests over the public network.

You can isolate this network traffic in your cluster by attaching a public gateway to only one subnet in your cluster. Then, you can use app affinity to deploy app pods that require access to external endpoints to only the subnet with an attached public gateway.

In VPC clusters, only one subnet exists per zone. When you attach a public gateway to only one subnet, and schedule app pods that require public access to only worker nodes on that subnet, these pods are isolated to one zone in your cluster.
{: note}

1. Target the region of the VPC that your cluster is deployed to.
  ```
  ibmcloud target -r <region>
  ```
  {: pre}

2. Check whether you have a public gateway in a zone where you have worker nodes. Within one VPC, you can create only one public gateway per zone.
  ```
  ibmcloud is public-gateways
  ```
  {: pre}

  Example output:
  ```
  ID                                     Name                                       VPC                          Zone         Floating IP                  Created                     Status      Resource group
  26426426-6065-4716-a90b-ac7ed7917c63   test-pgw                                   testvpc(36c8f522-.)          us-south-1   169.xx.xxx.xxx(26466378-.)   2019-09-20T16:27:32-05:00   available   -
  2ba2ba2b-fffa-4b0c-bdca-7970f09f9b8a   pgw-73b62bc0-b53a-11e9-9838-f3f4efa02374   team3(ff537d43-.)            us-south-2   169.xx.xxx.xxx(2ba9a280-.)   2019-08-02T10:30:29-05:00   available   -
  ```
  {: screen}
  * If you already have a public gateway in a zone where you have workers and in the VPC that your cluster is in, note the gateway's **ID**.
  * If you do not have a public gateway in a zone where you have workers and in the VPC that your cluster is in, create a public gateway. Consider naming the public gateway in the format `<cluster>-<zone>-gateway`. In the output, note the public gateway's **ID**.
    ```
    ibmcloud is public-gateway-create <gateway_name> <VPC_ID> <zone>
    ```
    {: pre}

    Example output:
    ```
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

3. List the worker nodes in your cluster. For the zone where you enabled the public gateway, note the **Primary IP** of one worker node.
  ```
  ibmcloud oc worker ls -c <cluster_name_or_ID>
  ```
  {: pre}

  Example output:
  ```
  ID                                                   Primary IP     Flavor   State    Status   Zone         Version
  kube-bl25g33d0if1cmfn0p8g-vpctest-default-000005ac   10.240.02.00   c2.2x4   normal   Ready    us-south-2   1.16.3
  kube-bl25g33d0if1cmfn0p8g-vpctest-default-00000623   10.240.01.00   c2.2x4   normal   Ready    us-south-1   1.16.3
  ```
  {: screen}

4. Describe the worker node. In the **Labels output**, note the subnet ID in the label `ibm-cloud.kubernetes.io/subnet-id`, such as `5f5787a4-f560-471b-b6ce-20067ac93439` in the following example.
  ```
  oc describe node <worker_primary_ip>
  ```
  {: pre}

  Example output:
  ```
  Name:               10.240.01.00
  Roles:              <none>
  Labels:             arch=amd64
                      beta.kubernetes.io/arch=amd64
                      beta.kubernetes.io/instance-type=c2.2x4
                      beta.kubernetes.io/os=linux
                      failure-domain.beta.kubernetes.io/region=us-south
                      failure-domain.beta.kubernetes.io/zone=us-south-1
                      ibm-cloud.kubernetes.io/ha-worker=true
                      ibm-cloud.kubernetes.io/iaas-provider=gc
                      ibm-cloud.kubernetes.io/internal-ip=10.240.0.77
                      ibm-cloud.kubernetes.io/machine-type=c2.2x4
                      ibm-cloud.kubernetes.io/os=UBUNTU_18_64
                      ibm-cloud.kubernetes.io/region=us-south
                      ibm-cloud.kubernetes.io/sgx-enabled=false
                      ibm-cloud.kubernetes.io/subnet-id=5f5787a4-f560-471b-b6ce-20067ac93439
                      ibm-cloud.kubernetes.io/worker-id=kube-bl25g33d0if1cmfn0p8g-vpcprod-default-00001093
                      ibm-cloud.kubernetes.io/worker-pool-id=bl25g33d0if1cmfn0p8g-5aa474f
                      ibm-cloud.kubernetes.io/worker-pool-name=default
                      ibm-cloud.kubernetes.io/worker-version=1.15.3_1517
                      ibm-cloud.kubernetes.io/zone=us-south-1
                      kubernetes.io/arch=amd64
                      kubernetes.io/hostname=10.240.0.77
                      kubernetes.io/os=linux
  Annotations:        node.alpha.kubernetes.io/ttl: 0
  ...
  ```
  {: screen}

5. Using the IDs of the public gateway and the subnet, attach the public gateway to the subnet. The worker nodes that are deployed to this subnet in this zone now have access to external endpoints.
  ```
  ibmcloud is subnet-update <subnet_ID> --public-gateway-id <gateway_ID>
  ```
  {: pre}

  Example output:
  ```
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

6. In the deployment file for your app, [add an affinity rule ![External link icon](../icons/launch-glyph.svg "External link icon")](https://kubernetes.io/docs/concepts/configuration/assign-pod-node/#node-affinity-beta-feature) for the subnet ID label that you found in step 4.

    In the **affinity** section of this example YAML, `ibm-cloud.kubernetes.io/subnet-id` is the `key` and `<subnet_ID>` is the `value`.
    ```
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: with-node-affinity
    spec:
      template:
        spec:
          affinity:
            nodeAffinity:
              requiredDuringSchedulingIgnoredDuringExecution:
                nodeSelectorTerms:
                - matchExpressions:
                  - key: ibm-cloud.kubernetes.io/subnet-id
                    operator: In
                    values:
                    - <subnet_ID>
    ...
    ```
    {: codeblock}

7. Apply the updated deployment configuration file.
    ```
    oc apply -f with-node-affinity.yaml
    ```
    {: pre}

8. Verify that the app pods deployed to the correct worker nodes.

    1. List the pods in your cluster. In the output, identify a pod for your app. Note the **NODE** private IP address of the worker node that the pod is on.
        ```
        oc get pods -o wide
        ```
        {: pre}

        In this example output, the app pod `cf-py-d7b7d94db-vp8pq` is on a worker node with the IP address `10.240.01.00`.
        ```
        NAME                   READY     STATUS              RESTARTS   AGE       IP               NODE
        cf-py-d7b7d94db-vp8pq  1/1       Running             0          15d       172.30.xxx.xxx   10.240.01.00
        ```
        {: screen}

    2. List the worker nodes in your cluster. In the output, look for the worker nodes in the zone where you attached the public gateway. Verify that the worker node with the private IP address that you identified in the previous step is deployed in this zone.

        ```
        ibmcloud oc worker ls --cluster <cluster_name_or_ID>
        ```
        {: pre}

        Example output:
        ```
        ID                                                   Primary IP     Flavor   State    Status   Zone         Version
        kube-bl25g33d0if1cmfn0p8g-vpctest-default-000005ac   10.240.02.00   c2.2x4   normal   Ready    us-south-2   1.16.3
        kube-bl25g33d0if1cmfn0p8g-vpctest-default-00000623   10.240.01.00   c2.2x4   normal   Ready    us-south-1   1.16.3
        ```
        {: screen}

9. Optional: If you use [access control lists (ACLs)](#acls) to control your cluster network traffic, create inbound and outbound rules in this subnet's ACL to allow ingress from and egress to the external public endpoints that your pods must access.

<br />


## Creating access control lists (ACLs) to control traffic to and from your cluster
{: #acls}

Control inbound and outbound traffic to your cluster by creating and applying ACLs to each subnet that your cluster is attached to.
{: shortdesc}

When you create a VPC, a default ACL is created in the format `allow-all-network-acl-<VPC_ID>` for the VPC. The ACL includes an inbound rule and an outbound rule that allow all traffic to and from your subnets. Any subnet that you create in the VPC is attached to this ACL by default. If you want to specify which traffic is permitted to the worker nodes on your VPC subnets, you can create a custom ACL for each subnet in the VPC.

For example, you can create the following set of ACL rules to block most inbound and outbound network traffic of a cluster, while allowing communication that is necessary for the cluster to function.

When you use the following steps to create custom ACLs, only network traffic that is specified in the ACL rules is permitted to and from your VPC subnets. All other traffic that is not specified in the ACLs is blocked for the subnets, such as cluster integrations with third party services. If you must allow other traffic to or from your worker nodes, you can add rules for that traffic in step 4.f.</br></br>ACL rules are applied to traffic in a specific order. If you want to add a rule after you complete the steps in this topic, ensure that you add the rule before the `deny-all-inbound` or `deny-all-outbound` rule. If you add a rule after these rules, your rule is ignored, because the packet matches the `deny-all-inbound` and `deny-all-outbound` rules and is blocked and removed before it can reach your rule. Create your rule in the proper order by running `ibmcloud is network-acl-rule-add <new_rule_name> $acl_id <allow|deny> <inbound|outbound> <protocol> <source_CIDR> <destination_CIDR> --before-rule-name deny-all-(inbound|outbound)`. For more information about ACL rule requirements and limitations, see [Working with ACLs and ACL rules](/docs/vpc-on-classic-network?topic=vpc-on-classic-network-setting-up-network-acls).
{: important}

1. Target the region of the VPC that your cluster is deployed to.
  ```
  ibmcloud target -r <region>
  ```
  {: pre}

2. List the worker nodes in your cluster. Note the ID of one worker node in each zone of your cluster.
  ```
  ibmcloud oc worker ls -c <cluster_name_or_ID>
  ```
  {: pre}

  Example output:
  ```
  ID                                                   Primary IP     Flavor   State    Status   Zone         Version
  kube-bl25g33d0if1cmfn0p8g-vpctest-default-000005ac   10.240.64.10   c2.2x4   normal   Ready    us-south-2   1.16.3
  kube-bl25g33d0if1cmfn0p8g-vpctest-default-00000623   10.240.0.5     c2.2x4   normal   Ready    us-south-1   1.16.3
  ```
  {: screen}

3. For one worker node in each zone, get the **ID** and **CIDR** of the subnet that the worker is attached to. After you complete this step for each zone where you have worker nodes, you have a list of the subnets that your cluster is attached to.
  ```
  ibmcloud oc worker get -c <cluster_name_or_ID> -w <worker_node_ID>
  ```
  {: pre}

  In this example output, the ID for the subnet in `us-south-1` is `a1b2c3d4-f560-471b-b6ce-20067ac93439` and the CIDR is `10.240.0.0/24`:
  ```
  Retrieving worker kube-bl25g33d0if1cmfn0p8g-vpctest-default-00000623...
  OK

  ID:                 kube-bl25g33d0if1cmfn0p8g-vpctest-default-00000623
  Zone:               us-south-1
  Worker Pool ID:     bl25g33d0if1cmfn0p8g-5aa474f
  Worker Pool Name:   default
  Flavor:             c2.2x4
  Version:            1.16.3

  Health
  State:     normal
  Message:   Ready

  Lifecycle
  State:      deployed
  Message:    -

  Subnets
  ID                                     IP Address               CIDR
  a1b2c3d4-f560-471b-b6ce-20067ac93439   10.240.0.67 (primary)    10.240.0.0/24
  ```
  {: screen}

4. For **each** subnet that you identified in the previous step, create a custom ACL with rules that limit inbound and outbound network traffic to only communication that is necessary for the cluster to function.

  1. Create an ACL. After you create the ACL, you can add rules to your ACL and apply the ACL to one subnet. Because the rules that you add to your ACL are specific to one subnet, consider naming the ACL in the format `<cluster>-<zone>-acl`, such as `mycluster-us-south-1-acl`, for easy identification. When you create the ACL, two rules are automatically created that allow all inbound and all outbound network traffic. In the output, note the ACL ID and the IDs of the two default rules.
    ```
    ibmcloud is network-acl-create <ACL_name>
    ```
    {: pre}

     Example output:
    ```
    Creating network ACL vpctest-us-south-1-acl under account Account as user user@email.com...

    ID        740b07cb-4e69-4ef2-b667-42ed27d8b29e
    Name      vpctest-us-south-1-acl
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

  2. Export the ACL ID as an environment variable.
    ```
    export acl_id=<ACL_ID>
    ```
    {: pre}

  3. Delete the default rules that allow all inbound and outbound traffic.
    ```
    ibmcloud is network-acl-rule-delete $acl_id <default_inbound_rule_ID> -f
    ```
    {: pre}
    ```
    ibmcloud is network-acl-rule-delete $acl_id <default_outbound_rule_ID> -f
    ```
    {: pre}

  4. Multizone clusters: Add rules to your ACL to allow worker nodes in one subnet to communicate with the worker nodes in all other subnets within the cluster. The subnet for which you create the ACL rule is defined as `0.0.0.0/0` and you use the CIDRs of the other subnets as your destination CIDR. Make sure to create one inbound and one outbound rule for each of the subnets that you want to connect to.
    ```
    ibmcloud is network-acl-rule-add allow-workers-outbound $acl_id allow outbound all 0.0.0.0/0 <other_zone_subnet_CIDR>
    ```
    {: pre}
    ```
    ibmcloud is network-acl-rule-add allow-workers-inbound $acl_id allow inbound all <other_zone_subnet_CIDR> 0.0.0.0/0
    ```
    {: pre}

  5. Create rules to allow inbound traffic from and outbound traffic to the `161.26.0.0/16` and `166.8.0.0/14` {{site.data.keyword.cloud_notm}} private subnets. The `161.26.0.0/16` rules allow you to create worker nodes in your cluster. The `166.8.0.0/14` rules allow worker nodes to communicate with the cluster master through the private service endpoint and to communicate with other {{site.data.keyword.cloud_notm}} services that support private service endpoints, such as {{site.data.keyword.registrylong_notm}}.

    <p class="tip">Need to connect your worker nodes to {{site.data.keyword.cloud_notm}} services that support only public service endpoints? [Attach a public gateway to the subnet ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/kubernetes/clusters) so that worker nodes can connect to a public external endpoint. Then, create inbound and outbound rules to allow ingress from and egress to the services' public service endpoints.</p>

    ```
    ibmcloud is network-acl-rule-add allow-ibm-private-network2-outbound $acl_id allow outbound all 0.0.0.0/0 161.26.0.0/16
    ibmcloud is network-acl-rule-add allow-ibm-private-network2-inbound $acl_id allow inbound all 161.26.0.0/16 0.0.0.0/0
    ibmcloud is network-acl-rule-add allow-ibm-private-network-outbound $acl_id allow outbound all 0.0.0.0/0 166.8.0.0/14
    ibmcloud is network-acl-rule-add allow-ibm-private-network-inbound $acl_id allow inbound all 166.8.0.0/14 0.0.0.0/0
    ```
    {: pre}

  6. If you must allow other traffic to or from your worker nodes on this subnet, add rules for that traffic.

    <p class="note">When you refer to the VPC subnet that your worker nodes are on, you must use `0.0.0.0/0`. For more tips on how to create your rule, see the [VPC CLI reference documentation](/docs/vpc-on-classic-network?topic=vpc-infrastructure-cli-plugin-vpc-reference#network-acl-rule-add).</p>

    ```
    ibmcloud is network-acl-rule-add <new_rule_name> $acl_id <allow|deny> <inbound|outbound> <protocol> <source_CIDR> <destination_CIDR>
    ```
    {: pre}

    For example, say that you want your worker nodes to communicate with a subnet in your organization's network, `207.42.8.0/24`. Your worker nodes must be able to both send and receive information from devices or services on this subnet. You can create an outbound rule for traffic to and an inbound rule for traffic from your organization's subnet:
    ```
    ibmcloud is network-acl-rule-add corporate-network-outbound $acl_id allow outbound all 0.0.0.0/0 207.42.8.0/24
    ibmcloud is network-acl-rule-add corporate-network-inbound $acl_id allow inbound all 207.42.8.0/24 0.0.0.0/0
    ```
    {: screen}

  7. Create rules to deny all other egress from and ingress to worker nodes that is not permitted by the previous rules that you created. Because these rules are created last in the chain of rules, they deny an incoming or outgoing connection only if the connection does not match any other rule that is earlier in the rule chain.
    ```
    ibmcloud is network-acl-rule-add deny-all-outbound $acl_id deny outbound all 0.0.0.0/0 0.0.0.0/0
    ibmcloud is network-acl-rule-add deny-all-inbound $acl_id deny inbound all 0.0.0.0/0 0.0.0.0/0
    ```
    {: pre}

  8. Apply this ACL to the subnet. When you apply this ACL, the rules that you defined are immediately applied to the worker nodes on the subnet.
    ```
    ibmcloud is subnet-update <subnet_ID> --network-acl-id $acl_id
    ```
    {: pre}

    Example output:
    ```
    ID                  a1b2c3d4-f560-471b-b6ce-20067ac93439
    Name                vpctest-us-south-1
    IPv*                ipv4
    IPv4 CIDR           10.240.0.0/24
    IPv6 CIDR           -
    Address Available   244
    Address Total       256
    ACL                 vpctest-us-south-1-acl(b664769d-514c-407f-a9f3-d44d72706121)
    Gateway             pgw-18a3ebb0-b539-11e9-9838-f3f4efa02374(f8b95e43-a408-4dc8-a489-ed649fc4cfec)
    Created             2019-08-02T10:20:17-05:00
    Status              available
    Zone                us-south-1
    VPC                 myvpc(ff537d43-a5a4-4b65-9627-17eddfa5237b)
    ```
    {: screen}

  9. Repeat these steps for each subnet.

<br />


## Creating Kubernetes policies to control traffic between pods
{: #kubernetes_policies}

Kubernetes policies protect pods from internal network traffic. You can create simple Kubernetes network policies to isolate app microservices from each other within a namespace or across namespaces.
{: shortdesc}

For more information about how Kubernetes network policies control pod-to-pod traffic and for more example policies, see the [Kubernetes documentation ![External link icon](../icons/launch-glyph.svg "External link icon")](https://kubernetes.io/docs/concepts/services-networking/network-policies/).
{: tip}

### Isolate app services within a namespace
{: #vpc-services_one_ns}

The following scenario demonstrates how to manage traffic between app microservices within one namespace.

An Accounts team deploys multiple app services in one namespace, but they need isolation to permit only necessary communication between the microservices over the public network. For the app `Srv1`, the team has front end, back end, and database services. They label each service with the `app: Srv1` label and the `tier: frontend`, `tier: backend`, or `tier: db` label.

<img src="images/cs_network_policy_single_ns.png" width="200" alt="Use a network policy to manage cross-namespace traffic." style="width:200px; border-style: none"/>

The Accounts team wants to allow traffic from the front end to the back end, and from the back end to the database. They use labels in their network policies to designate which traffic flows are permitted between microservices.

First, they create a Kubernetes network policy that allows traffic from the front end to the back end:

```
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

```
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
{: #vpc-services_across_ns}

The following scenario demonstrates how to manage traffic between app microservices across multiple namespaces.

Services that are owned by different subteams need to communicate, but the services are deployed in different namespaces within the same cluster. The Accounts team deploys front end, back end, and database services for the app Srv1 in the accounts namespace. The Finance team deploys front end, back end, and database services for the app Srv2 in the finance namespace. Both teams label each service with the `app: Srv1` or `app: Srv2` label and the `tier: frontend`, `tier: backend`, or `tier: db` label. They also label the namespaces with the `usage: accounts` or `usage: finance` label.

<img src="images/cs_network_policy_multi_ns.png" width="475" alt="Use a network policy to manage cross-namepsace traffic." style="width:475px; border-style: none"/>

The Finance team's Srv2 needs to call information from the Accounts team's Srv1 back end. So the Accounts team creates a Kubernetes network policy that uses labels to allow all traffic from the finance namespace to the Srv1 back end in the accounts namespace. The team also specifies the port 3111 to isolate access through that port only.

```
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


</ff-roks311-vpc>
