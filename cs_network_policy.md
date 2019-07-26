---

copyright:
  years: 2014, 2019
lastupdated: "2019-07-26"

keywords: kubernetes, iks

subcollection: containers

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

# Controlling traffic with network policies
{: #network_policies}

Every {{site.data.keyword.containerlong}} cluster is set up with a network plug-in called Calico. Default network policies are set up to secure the public network interface of every worker node in the cluster.
{: shortdesc}

If you have unique security requirements or you have a multizone cluster with VLAN spanning enabled, you can use Calico and Kubernetes to create network policies for a cluster. With Kubernetes network policies, you can specify the network traffic that you want to allow or block to and from a pod within a cluster. To set more advanced network policies such as blocking inbound (ingress) traffic to network load balancer (NLB) services, use Calico network policies.

* [Kubernetes network policies ![External link icon](../icons/launch-glyph.svg "External link icon")](https://kubernetes.io/docs/concepts/services-networking/network-policies/): These policies specify how pods can communicate with other pods and with external endpoints. As of Kubernetes version 1.8, both incoming and outgoing network traffic can be allowed or blocked based on protocol, port, and source or destination IP addresses. Traffic can also be filtered based on pod and namespace labels. Kubernetes network policies are applied by using `{[kubectl]}` commands or the Kubernetes APIs. When these policies are applied, they are automatically converted into Calico network policies and Calico enforces these policies.
* [Calico network policies ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.projectcalico.org/v3.3/getting-started/bare-metal/policy/): These policies are a superset of the Kubernetes network policies and are applied by using `calicoctl` commands. Calico policies add the following features.
  * Allow or block network traffic on specific network interfaces regardless of the Kubernetes pod source or destination IP address or CIDR.
  * Allow or block network traffic for pods across namespaces.
  * [Block inbound traffic to Kubernetes LoadBalancer or NodePort services](#block_ingress).

Calico enforces these policies, including any Kubernetes network policies that are automatically converted to Calico policies, by setting up Linux Iptables rules on the Kubernetes worker nodes. Iptables rules serve as a firewall for the worker node to define the characteristics that the network traffic must meet to be forwarded to the targeted resource.

To use network load balancer (NLB) and Ingress application load balancer (ALB) services, use Calico and Kubernetes policies to manage network traffic into and out of your cluster. Do not use IBM Cloud infrastructure [security groups](/docs/infrastructure/security-groups?topic=security-groups-about-ibm-security-groups#about-ibm-security-groups). IBM Cloud infrastructure security groups are applied to the network interface of a single virtual server to filter traffic at the hypervisor level. However, security groups do not support the VRRP protocol, which {{site.data.keyword.containerlong_notm}} must use to manage the ALB and NLB IP addresses. If the VRRP protocol is not present to manage the IP, ALB and NLB services do not work properly.
{: tip}

<br />


## Default Calico and Kubernetes network policies
{: #default_policy}

When a cluster with a public VLAN is created, a `HostEndpoint` resource with the `ibm.role: worker_public` label is created automatically for each worker node and its public network interface. To protect the public network interface of a worker node, default Calico policies are applied to any host endpoint with the `ibm.role: worker_public` label.
{:shortdesc}

These default Calico host policies allow all outbound network traffic and allow inbound traffic to specific cluster components, such as Kubernetes NodePort, LoadBalancer, and Ingress services. Any other inbound network traffic from the internet to your worker nodes that isn't specified in the default policies is blocked. The default policies don't affect pod to pod traffic.

Review the following default Calico host policies that are automatically applied to your cluster.

Do not remove policies that are applied to a host endpoint unless you fully understand the policy. Be sure that you do not need the traffic that is being allowed by the policy.
{: important}

 <table summary="The first row in the table spans both columns. Read the rest of the rows from left to right, with the server zone in column one and IP addresses to match in column two.">
 <caption>Default Calico host policies for each cluster</caption>
  <thead>
  <th colspan=2><img src="images/idea.png" alt="Idea icon"/> Default Calico host policies for each cluster</th>
  </thead>
  <tbody>
    <tr>
      <td><code>allow-all-outbound</code></td>
      <td>Allows all outbound traffic.</td>
    </tr>
    <tr>
      <td><code>allow-bigfix-port</code></td>
      <td>Allows incoming traffic on port 52311 to the BigFix app to allow necessary worker node updates.</td>
    </tr>
    <tr>
      <td><code>allow-icmp</code></td>
      <td>Allows incoming ICMP packets (pings).</td>
     </tr>
    <tr>
      <td><code>allow-node-port-dnat</code></td>
      <td>Allows incoming network load balancer (NLB), Ingress application load balancer (ALB), and NodePort service traffic to the pods that those services are exposing. <strong>Note</strong>: You don't need to specify the exposed ports because Kubernetes uses destination network address translation (DNAT) to forward the service requests to the correct pods. That forwarding takes place before the host endpoint policies are applied in Iptables.</td>
   </tr>
   <tr>
      <td><code>allow-sys-mgmt</code></td>
      <td>Allows incoming connections for specific IBM Cloud infrastructure systems that are used to manage the worker nodes.</td>
   </tr>
   <tr>
    <td><code>allow-vrrp</code></td>
    <td>Allow VRRP packets, which are used to monitor and move virtual IP addresses between worker nodes.</td>
   </tr>
  </tbody>
</table>

A default Kubernetes policy that limits access to the Kubernetes Dashboard is also created. Kubernetes policies don't apply to the host endpoint, but to the `kube-dashboard` pod instead. This policy applies to clusters that are connected only to a private VLAN and clusters that are connected to a public and private VLAN.

<table>
<caption>Default Kubernetes policies for each cluster</caption>
<thead>
<th colspan=2><img src="images/idea.png" alt="Idea icon"/> Default Kubernetes policies for each cluster</th>
</thead>
<tbody>
 <tr>
  <td><code>kubernetes-dashboard</code></td>
  <td>Provided in the <code>kube-system</code> namespace: Blocks all pods from accessing the Kubernetes Dashboard. This policy does not impact accessing the dashboard from the {{site.data.keyword.cloud_notm}} console or by using <code>{[kubectl]} proxy</code>. If a pod requires access to the dashboard, deploy the pod in a namespace that has the <code>kubernetes-dashboard-policy: allow</code> label.</td>
 </tr>
</tbody>
</table>

<br />


## Installing and configuring the Calico CLI
{: #cli_install}

To view, manage, and add Calico policies, install and configure the Calico CLI.
{:shortdesc}

1. [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure) Include the `--admin` and `--network` options with the `ibmcloud ks cluster-config` command. `--admin` downloads the keys to access your infrastructure portfolio and run Calico commands on your worker nodes. `--network` downloads the Calico configuration file to run all Calico commands.

  ```
  ibmcloud ks cluster-config --cluster <cluster_name_or_ID> --admin --network
  ```
  {: pre}

3. For OS X and Linux users, complete the following steps.
    1. Create the `/etc/calico` directory.
        ```
        sudo mkdir /etc/calico
        ```
        {: pre}

    2. Move the Calico configuration file that you previously downloaded to the directory.
        ```
        sudo mv /Users/<user>/.bluemix/plugins/container-service/clusters/<cluster_name>-admin/calicoctl.cfg /etc/calico
        ```
        {: pre}

4. [Download the Calico CLI ![External link icon](../icons/launch-glyph.svg "External link icon")](https://github.com/projectcalico/calicoctl/releases).

    If you are using OS X, download the `-darwin-amd64` version. If you are using Windows, install the Calico CLI in the same directory as the {{site.data.keyword.cloud_notm}} CLI. This setup saves you some file path changes when you run commands later. Make sure to save the file as `calicoctl.exe`.
    {: tip}

5. For OS X and Linux users, complete the following steps.
    1. Move the executable file to the _/usr/local/bin_ directory.
        - Linux:

          ```
          mv filepath/calicoctl /usr/local/bin/calicoctl
          ```
          {: pre}

        - OS X:

          ```
          mv filepath/calicoctl-darwin-amd64 /usr/local/bin/calicoctl
          ```
          {: pre}

    2. Make the file an executable file.

        ```
        chmod +x /usr/local/bin/calicoctl
        ```
        {: pre}

6. If corporate network policies use proxies or firewalls to prevent access from your local system to public endpoints, [allow TCP access for Calico commands](/docs/containers?topic=containers-firewall#firewall).

7. Verify that the Calico configuration is working correctly.

    - Linux and OS X:

      ```
      calicoctl get nodes
      ```
      {: pre}

    - Windows: Use the `--config` flag to point to the network configuration file that you got in step 1. Include this flag each time you run a `calicoctl` command.

      ```
      calicoctl get nodes --config=<filepath>/calicoctl.cfg
      ```
      {: pre}

      Output:

      ```
      NAME
      kube-dal10-crc21191ee3997497ca90c8173bbdaf560-w1.cloud.ibm
      kube-dal10-crc21191ee3997497ca90c8173bbdaf560-w2.cloud.ibm
      kube-dal10-crc21191ee3997497ca90c8173bbdaf560-w3.cloud.ibm
      ```
      {: screen}

<br />


## Viewing network policies
{: #view_policies}

View the details for default and any added network policies that are applied to your cluster.
{:shortdesc}

Before you begin:
1. [Install and configure the Calico CLI.](#cli_install)
2. [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure) Include the `--admin` and `--network` options with the `ibmcloud ks cluster-config` command. `--admin` downloads the keys to access your infrastructure portfolio and run Calico commands on your worker nodes. `--network` downloads the Calico configuration file to run all Calico commands.

  ```
  ibmcloud ks cluster-config --cluster <cluster_name_or_ID> --admin --network
  ```
  {: pre}

**To view network policies in clusters**:

Linux and Mac users don't need to include the `--config=<filepath>/calicoctl.cfg` flag in `calicoctl` commands.
{: tip}

1. View the Calico host endpoint.

    ```
    calicoctl get hostendpoint -o yaml --config=<filepath>/calicoctl.cfg
    ```
    {: pre}

2. View all of the Calico and Kubernetes network policies that were created for the cluster. This list includes policies that might not be applied to any pods or hosts yet. For a network policy to be enforced, a Kubernetes resource must be found that matches the selector that was defined in the Calico network policy.

    [Network policies ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.projectcalico.org/v3.3/reference/calicoctl/resources/networkpolicy) are scoped to specific namespaces:
    ```
    calicoctl get NetworkPolicy --all-namespaces -o wide --config=<filepath>/calicoctl.cfg
    ```
    {:pre}

    [Global network policies ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.projectcalico.org/v3.3/reference/calicoctl/resources/globalnetworkpolicy) are not scoped to specific namespaces:
    ```
    calicoctl get GlobalNetworkPolicy -o wide --config=<filepath>/calicoctl.cfg
    ```
    {: pre}

3. View details for a network policy.

    ```
    calicoctl get NetworkPolicy -o yaml <policy_name> --namespace <policy_namespace> --config=<filepath>/calicoctl.cfg
    ```
    {: pre}

4. View the details of all global network policies for the cluster.

    ```
    calicoctl get GlobalNetworkPolicy -o yaml --config=<filepath>/calicoctl.cfg
    ```
    {: pre}

<br />


## Adding network policies
{: #adding_network_policies}

In most cases, the default policies do not need to be changed. Only advanced scenarios might require changes. If you find that you must make changes, you can create your own network policies.
{:shortdesc}

To create Kubernetes network policies, see the [Kubernetes network policy documentation ![External link icon](../icons/launch-glyph.svg "External link icon")](https://kubernetes.io/docs/concepts/services-networking/network-policies/).

To create Calico policies, use the following steps.

1. [Install and configure the Calico CLI.](#cli_install)
2. [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure) Include the `--admin` and `--network` options with the `ibmcloud ks cluster-config` command. `--admin` downloads the keys to access your infrastructure portfolio and run Calico commands on your worker nodes. `--network` downloads the Calico configuration file to run all Calico commands.

  ```
  ibmcloud ks cluster-config --cluster <cluster_name_or_ID> --admin --network
  ```
  {: pre}

3. Define your Calico [network policy ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.projectcalico.org/v3.3/reference/calicoctl/resources/networkpolicy) or [global network policy ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.projectcalico.org/v3.3/reference/calicoctl/resources/globalnetworkpolicy) by creating a configuration script (`.yaml`) with Calico v3 policy syntax. These configuration files include the selectors that describe what pods, namespaces, or hosts that these policies apply to. Refer to these [sample Calico policies ![External link icon](../icons/launch-glyph.svg "External link icon")](http://docs.projectcalico.org/v3.3/getting-started/kubernetes/tutorials/advanced-policy) to help you create your own.

4. Apply the policies to the cluster.
    - Linux and OS X:

      ```
      calicoctl apply -f policy.yaml
      ```
      {: pre}

    - Windows:

      ```
      calicoctl apply -f filepath/policy.yaml --config=<filepath>/calicoctl.cfg
      ```
      {: pre}

<br />


## Controlling inbound traffic to NLB or NodePort services
{: #block_ingress}

[By default](#default_policy), Kubernetes NodePort and LoadBalancer services are designed to make your app available on all public and private cluster interfaces. However, you can use Calico policies to block incoming traffic to your services based on traffic source or destination.
{:shortdesc}

Default Kubernetes and Calico policies are difficult to apply to protecting Kubernetes NodePort and LoadBalancer services due to the DNAT Iptables rules generated for these services. However, pre-DNAT policies prevent specified traffic from reaching your apps because they generate and apply Iptables rules before Kubernetes uses regular DNAT to forward traffic to pods.

Some common uses for Calico pre-DNAT network policies:

  - Block traffic to public node ports of a private network load balancer (NLB) service: An NLB service makes your app available over the NLB IP address and port and makes your app available over the service's node ports. Node ports are accessible on every IP address (public and private) for every node within the cluster.
  - Block traffic to public node ports on clusters that are running [edge worker nodes](/docs/containers?topic=containers-edge#edge): Blocking node ports ensures that the edge worker nodes are the only worker nodes that handle incoming traffic.
  - Block traffic from certain source IP addresses or CIDRs (blacklisting)
  - Allow traffic from only certain source IP addresses or CIDRs (whitelisting), and block all other traffic

To see how to whitelist or blacklist source IP addresses, try the [Using Calico network policies to block traffic tutorial](/docs/containers?topic=containers-policy_tutorial#policy_tutorial). For more example Calico network policies that control traffic to and from your cluster, you can check out the [stars policy demo ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.projectcalico.org/v3.3/getting-started/kubernetes/tutorials/stars-policy/) and the [advanced network policy ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.projectcalico.org/v3.3/getting-started/kubernetes/tutorials/advanced-policy).
{: tip}

Before you begin:
1. [Install and configure the Calico CLI.](#cli_install)
2. [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure) Include the `--admin` and `--network` options with the `ibmcloud ks cluster-config` command. `--admin` downloads the keys to access your infrastructure portfolio and run Calico commands on your worker nodes. `--network` downloads the Calico configuration file to run all Calico commands.

  ```
  ibmcloud ks cluster-config --cluster <cluster_name_or_ID> --admin --network
  ```
  {: pre}

To create a pre-DNAT policy:

1. Define a Calico pre-DNAT network policy for ingress (inbound traffic) access to Kubernetes services.
    * Use [Calico v3 policy syntax ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.projectcalico.org/v3.3/reference/calicoctl/resources/networkpolicy).
    * If you manage traffic to an [NLB 2.0](/docs/containers?topic=containers-loadbalancer-about#planning_ipvs), you must include the `applyOnForward: true` and `doNotTrack: true` fields to the `spec` section of the policy.

        Example resource that blocks all node ports:

        ```
        apiVersion: projectcalico.org/v3
        kind: GlobalNetworkPolicy
        metadata:
          name: deny-nodeports
        spec:
          applyOnForward: true
          preDNAT: true
          ingress:
          - action: Deny
            destination:
              ports:
              - 30000:32767
            protocol: TCP
            source: {}
          - action: Deny
            destination:
              ports:
              - 30000:32767
            protocol: UDP
            source: {}
          selector: ibm.role=='worker_public'
          order: 1100
          types:
          - Ingress
        ```
        {: codeblock}

        Example resource that whitelists traffic from only a specified source CIDR to an NLB 2.0:

        ```
        apiVersion: projectcalico.org/v3
        kind: GlobalNetworkPolicy
        metadata:
          name: whitelist
        spec:
          applyOnForward: true
          doNotTrack: true
          ingress:
          - action: Allow
            destination:
              nets:
              - <loadbalancer_IP>/32
              ports:
              - 80
            protocol: TCP
            source:
              nets:
              - <client_address>/32
          selector: ibm.role=='worker_public'
          order: 500
          types:
          - Ingress
        ```
        {: codeblock}

        Example resource that whitelists traffic from only a specified source CIDR to an NLB 1.0:

        ```
        apiVersion: projectcalico.org/v3
        kind: GlobalNetworkPolicy
        metadata:
          name: whitelist
        spec:
          applyOnForward: true
          preDNAT: true
          ingress:
          - action: Allow
            destination:
              nets:
              - <loadbalancer_IP>/32
              ports:
              - 80
            protocol: TCP
            source:
              nets:
              - <client_address>/32
          selector: ibm.role=='worker_public'
          order: 500
          types:
          - Ingress
        ```
        {: codeblock}

2. Apply the Calico preDNAT network policy. It takes about 1 minute for the
policy changes to be applied throughout the cluster.

  - Linux and OS X:

    ```
    calicoctl apply -f deny-nodeports.yaml
    ```
    {: pre}

  - Windows:

    ```
    calicoctl apply -f filepath/deny-nodeports.yaml --config=<filepath>/calicoctl.cfg
    ```
    {: pre}

3. Optional: In multizone clusters, a multizone load balancer (MZLB) health checks the Ingress application load balancers (ALBs) in each zone of your cluster and keeps the DNS lookup results updated based on these health checks. If you use pre-DNAT policies to block all incoming traffic to Ingress services, you must also whitelist [Cloudflare's IPv4 IPs ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.cloudflare.com/ips/) that are used to check the health of your ALBs. For steps on how to create a Calico pre-DNAT policy to whitelist these IPs, see Lesson 3 of the [Calico network policy tutorial](/docs/containers?topic=containers-policy_tutorial#lesson3).

## Isolating clusters on the public network
{: #isolate_workers_public}

You can isolate your cluster on the public network by applying [Calico public network policies ![External link icon](../icons/launch-glyph.svg "External link icon")](https://github.com/IBM-Cloud/kube-samples/tree/master/calico-policies/public-network-isolation).
{: shortdesc}

This set of Calico policies work in conjunction with the [default Calico policies](#default_policy) to block most public network traffic of a cluster while allowing communication that is necessary for the cluster to function to specific subnets. To see a list of the ports that are opened by these policies and a list of the policies that are included, see the [README for the Calico public network policies ![External link icon](../icons/launch-glyph.svg "External link icon")](https://github.com/IBM-Cloud/kube-samples/blob/master/calico-policies/public-network-isolation/README.md).

When you apply the egress pod policies that are included in this policy set, only network traffic to the subnets and ports that are specified in the pod policies is permitted. All traffic to any subnets or ports that are not specified in the policies is blocked for all pods in all namespaces. Because only the ports and subnets that are necessary for the pods to function in {{site.data.keyword.containerlong_notm}} are specified in these policies, your pods cannot send network traffic over the internet until you add or change the Calico policy to allow them to.
{: important}

Before you begin:
1. [Install and configure the Calico CLI.](#cli_install)
2. [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure) Include the `--admin` and `--network` options with the `ibmcloud ks cluster-config` command. `--admin` downloads the keys to access your infrastructure portfolio and run Calico commands on your worker nodes. `--network` downloads the Calico configuration file to run all Calico commands.
  ```
  ibmcloud ks cluster-config --cluster <cluster_name_or_ID> --admin --network
  ```
  {: pre}

To protect your cluster on the public network by using Calico policies:

1. Clone the `IBM-Cloud/kube-samples` repository.
  ```
  git clone https://github.com/IBM-Cloud/kube-samples.git
  ```
  {: pre}

2. Navigate to the public policy directory for the region that your cluster is in. Example command for a cluster in US South:
  ```
  cd <filepath>/IBM-Cloud/kube-samples/calico-policies/public-network-isolation/us-south
  ```
  {: pre}

3. Apply the policies.
  ```
  calicoctl apply -f allow-egress-pods-public.yaml --config=<filepath>/calicoctl.cfg
  calicoctl apply -f allow-ibm-ports-public.yaml --config=<filepath>/calicoctl.cfg
  calicoctl apply -f allow-public-service-endpoint.yaml --config=<filepath>/calicoctl.cfg
  calicoctl apply -f deny-all-outbound.yaml --config=<filepath>/calicoctl.cfg
  ```
  {: pre}

4. Optional: To allow your worker nodes to access other {{site.data.keyword.Bluemix_notm}} services over the public network, apply the `allow-public-services.yaml` and `allow-public-services-pods.yaml` policies. The policy allows access to the IP addresses for {{site.data.keyword.registryshort_notm}}, and if the services are available in the region, {{site.data.keyword.la_full_notm}} and {{site.data.keyword.mon_full_notm}}. To access other IBM Cloud services, you must manually add the subnets for those services to this policy.
  ```
  calicoctl apply -f allow-public-services.yaml --config=<filepath>/calicoctl.cfg
  calicoctl apply -f allow-public-services-pods.yaml --config=<filepath>/calicoctl.cfg
  ```
  {: pre}

5. Verify that the policies are applied.
  ```
  calicoctl get GlobalNetworkPolicies -o yaml --config=<filepath>/calicoctl.cfg
  ```
  {: pre}

<br />


## Isolating clusters on the private network
{: #isolate_workers}

You can isolate your cluster from other systems on the private network by applying [Calico private network policies ![External link icon](../icons/launch-glyph.svg "External link icon")](https://github.com/IBM-Cloud/kube-samples/tree/master/calico-policies/private-network-isolation/calico-v3).
{: shortdesc}

This set of Calico policies and host endpoints can isolate the private network traffic of a cluster from other resources in the account's private network, while allowing communication on the private network that is necessary for the cluster to function. For example, when you enable [VRF or VLAN spanning](/docs/containers?topic=containers-plan_clusters#worker-worker) to allow worker nodes to communicate with each other on the private network, any instance that is connected to any of the private VLANs in the same {{site.data.keyword.Bluemix_notm}} account can communicate with your worker nodes.

To see a list of the ports that are opened by these policies and a list of the policies that are included, see the [README for the Calico public network policies ![External link icon](../icons/launch-glyph.svg "External link icon")](https://github.com/IBM-Cloud/kube-samples/blob/master/calico-policies/private-network-isolation/README.md).

When you apply the egress pod policies that are included in this policy set, only network traffic to the subnets and ports that are specified in the pod policies is permitted. All traffic to any subnets or ports that are not specified in the policies is blocked for all pods in all namespaces. Because only the ports and subnets that are necessary for the pods to function in {{site.data.keyword.containerlong_notm}} are specified in these policies, your pods cannot send network traffic over the private network until you add or change the Calico policy to allow them to.
{: important}

Before you begin:
1. [Install and configure the Calico CLI.](#cli_install)
2. [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure) Include the `--admin` and `--network` options with the `ibmcloud ks cluster-config` command. `--admin` downloads the keys to access your infrastructure portfolio and run Calico commands on your worker nodes. `--network` downloads the Calico configuration file to run all Calico commands.

  ```
  ibmcloud ks cluster-config --cluster <cluster_name_or_ID> --admin --network
  ```
  {: pre}

To isolate your cluster on the private network by using Calico policies:

1. Clone the `IBM-Cloud/kube-samples` repository.
  ```
  git clone https://github.com/IBM-Cloud/kube-samples.git
  ```
  {: pre}

2. Navigate to the `calico-v3` private policy directory for the region that your cluster is in. Example command for a cluster in US South:
  ```
  cd <filepath>/IBM-Cloud/kube-samples/calico-policies/private-network-isolation/calico-v3/us-south
  ```
  {: pre}

3. Set up private host endpoints for your worker nodes. When your worker nodes have private host endpoints, the policies that you apply in the next several steps can target the worker node private interface (eth0) and the pod network of a cluster.
  1. Open the `generic-privatehostendpoint.yaml` policy.
  2. Replace `<worker_name>` with the name of a worker node.
    <p class="note">Some worker nodes must follow a different naming structure for Calico policies. You must use the name that is returned when you run `calicoctl get nodes --config=<filepath>/calicoctl.cfg`.</p>
  3. Replace `<worker-node-private-ip>` with the private IP address for the worker node. To see your worker nodes' private IPs, run `ibmcloud ks workers --cluster <my_cluster>`.
  4. For each worker node in your cluster, repeat these steps in a separate entry in the file.
    <p class="important">Each time you add a worker node to a cluster, you must update the host endpoints file with the new entries.</p>
  5. Save the policy.

4. Apply the policies.
  ```
  calicoctl apply -f generic-privatehostendpoint.yaml --config=<filepath>/calicoctl.cfg
  calicoctl apply -f allow-all-workers-private.yaml --config=<filepath>/calicoctl.cfg
  calicoctl apply -f allow-egress-pods-private.yaml --config=<filepath>/calicoctl.cfg
  calicoctl apply -f allow-ibm-ports-private.yaml --config=<filepath>/calicoctl.cfg
  calicoctl apply -f allow-icmp-private.yaml --config=<filepath>/calicoctl.cfg
  calicoctl apply -f allow-private-service-endpoint.yaml --config=<filepath>/calicoctl.cfg
  calicoctl apply -f allow-sys-mgmt-private.yaml --config=<filepath>/calicoctl.cfg
  ```
  {: pre}

5. Optional: To allow your workers and pods to access {{site.data.keyword.registryshort_notm}} over the private network, apply the `allow-private-services.yaml` and `allow-private-services-pods.yaml` policies. To access other IBM Cloud services that support private service endpoints, you must manually add the subnets for those services to this policy.
  ```
  calicoctl apply -f allow-private-services.yaml --config=<filepath>/calicoctl.cfg
  calicoctl apply -f allow-private-services-pods.yaml --config=<filepath>/calicoctl.cfg
  ```
  {: pre}

6. Optional: To expose your apps with private network load balancers (NLBs) or Ingress application load balancers (ALBs), you must open the VRRP protocol by applying the `allow-vrrp-private` policy.
  ```
  calicoctl apply -f allow-vrrp-private.yaml --config=<filepath>/calicoctl.cfg
  ```
  {: pre}
  You can further control access to networking services by creating [Calico pre-DNAT policies](/docs/containers?topic=containers-network_policies#block_ingress). In the pre-DNAT policy, ensure that you use `selector: ibm.role=='worker_private'` to apply the policy to the workers' private host endpoints.
  {: tip}

7. Verify that the policies are applied.
  ```
  calicoctl get GlobalNetworkPolicies -o yaml --config=<filepath>/calicoctl.cfg
  ```
  {: pre}

<br />


## Controlling traffic between pods
{: #isolate_services}

Kubernetes policies protect pods from internal network traffic. You can create simple Kubernetes network policies to isolate app microservices from each other within a namespace or across namespaces.
{: shortdesc}

For more information about how Kubernetes network policies control pod-to-pod traffic and for more example policies, see the [Kubernetes documentation ![External link icon](../icons/launch-glyph.svg "External link icon")](https://kubernetes.io/docs/concepts/services-networking/network-policies/).
{: tip}

### Isolate app services within a namespace
{: #services_one_ns}

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
{: #services_across_ns}

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

<br />


## Logging denied traffic
{: #log_denied}

To log denied traffic requests to certain pods in your cluster, you can create a Calico log network policy.
{: shortdesc}

When you set up network policies to limit traffic to app pods, traffic requests that are not permitted by these policies are denied and dropped. In some scenarios, you might want more information about denied traffic requests. For example, you might notice some unusual traffic that is continuously being denied by one of your network policies. To monitor the potential security threat, you can set up logging to record every time that the policy denies an attempted action on specified app pods.

This section shows you how to log traffic that is denied by a Kubernetes network policy. To log traffic that is denied by a Calico network policy, see [Lesson 5 of the Calico network policy tutorial](/docs/containers?topic=containers-policy_tutorial#lesson5).
{: tip}

Before you begin:
1. [Install and configure the Calico CLI.](#cli_install)
2. [Target the Kubernetes CLI to the cluster](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure). Include the `--admin` option with the `ibmcloud ks cluster-config` command, which is used to download the certificates and permission files. This download also includes the keys to access your infrastructure portfolio and run Calico commands on your worker nodes.
    ```
    ibmcloud ks cluster-config --cluster <cluster_name> --admin
    ```
    {: pre}

To log denied traffic:

1. Create or use an existing Kubernetes network policy that blocks or limits incoming traffic.
  1. Create a Kubernetes network policy. For example, to control traffic between pods, you might use the following example Kubernetes policy that is named `access-nginx` that limits access to an NGINX app. Incoming traffic to pods that are labeled "run=nginx" is allowed only from pods with the "run=access" label. All other incoming traffic to the "run=nginx" app pods is blocked.
    ```
    kind: NetworkPolicy
    apiVersion: networking.k8s.io/v1
    metadata:
      name: access-nginx
    spec:
      podSelector:
        matchLabels:
          run: nginx
      ingress:
        - from:
          - podSelector:
              matchLabels:
                run: access
    ```
    {: codeblock}

  2. Apply the policy.
    ```
    {[kubectl]} apply -f <policy_name>.yaml
    ```
    {: pre}

  3. The Kubernetes policy is automatically converted to a Calico NetworkPolicy so that Calico can apply it as Iptables rules. Review the syntax of the automatically created Calico policy and copy the value of the `spec.selector` field.
    ```
    calicoctl get policy -o yaml <policy_name> --config=<filepath>/calicoctl.cfg
    ```
    {: pre}

    For example, after the Kubernetes policy is applied and converted to a Calico NetworkPolicy, the `access-nginx` policy has the following Calico v3 syntax. The `spec.selector` field has the value `projectcalico.org/orchestrator == 'k8s' && run == 'nginx'`.
    ```
    apiVersion: projectcalico.org/v3
    kind: NetworkPolicy
    metadata:
      name: access-nginx
    spec:
      ingress:
      - action: Allow
        destination: {}
        source:
          selector: projectcalico.org/orchestrator == 'k8s' && run == 'access'
      order: 1000
      selector: projectcalico.org/orchestrator == 'k8s' && run == 'nginx'
      types:
      - Ingress
    ```
    {: screen}

2. To log all the traffic that is denied by the policy you created in the previous step, create a Calico NetworkPolicy named `log-denied-packets`. For example, the following log policy uses the same pod selector as the example `access-nginx` Kubernetes policy described in step 1, which adds this policy to the Calico Iptables rule chain. By using a higher-order number, such as `3000`, you can ensure that this rule is added to the end of the Iptables rule chain. Any request packet from the `run=access`-labeled pod that matches the `access-nginx` policy rule is accepted by the `run=nginx`-labeled pods. However, when packets from any other source try to match the low-order `access-nginx` policy rule, they are denied. Those packets then try to match the high-order `log-denied-packets` policy rule. `log-denied-packets` logs any packets that arrive to it, so only packets that were denied by the `run=nginx`-labeled pods are logged. After the packets' attempts are logged, the packets are dropped.
  ```
  apiVersion: projectcalico.org/v3
  kind: NetworkPolicy
  metadata:
    name: log-denied-packets
  spec:
    types:
    - Ingress
    ingress:
    - action: Log
      destination: {}
      source: {}
    selector: projectcalico.org/orchestrator == 'k8s' && run == 'nginx'
    order: 3000
  ```
  {: codeblock}

  <table>
  <caption>Understanding the log policy YAML components</caption>
  <thead>
  <th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding the log policy YAML components</th>
  </thead>
  <tbody>
  <tr>
   <td><code>types</code></td>
   <td>This <code>Ingress</code> policy applies to all incoming traffic requests. The value <code>Ingress</code> is a general term for all incoming traffic, and does not refer to traffic only from the IBM Ingress ALB.</td>
  </tr>
   <tr>
    <td><code>ingress</code></td>
    <td><ul><li><code>action</code>: The <code>Log</code> action writes a log entry for any requests that match this policy to the `/var/log/syslog` path on the worker node.</li><li><code>destination</code>: No destination is specified because the <code>selector</code> applies this policy to all pods with a certain label.</li><li><code>source</code>: This policy applies to requests from any source.</li></ul></td>
   </tr>
   <tr>
    <td><code>selector</code></td>
    <td>Replace &lt;selector&gt; with the same selector in the `spec.selector` field that you used in your policy from step 1. For example, by using the selector <code>selector: projectcalico.org/orchestrator == 'k8s' && run == 'nginx'</code>, this policy's rule is added to the same Iptables chain as the <code>access-nginx</code> sample Kubernetes network policy rule in step 1. This policy applies only to incoming network traffic to pods that use the same selector label.</td>
   </tr>
   <tr>
    <td><code>order</code></td>
    <td>Calico policies have orders that determine when they are applied to incoming request packets. Policies with lower orders, such as <code>1000</code>, are applied first. Policies with higher orders are applied after the lower-order policies. For example, a policy with a very high order, such as <code>3000</code>, is effectively applied last after all the lower-order policies have been applied.</br></br>Incoming request packets go through the Iptables rules chain and try to match rules from lower-order policies first. If a packet matches any rule, the packet is accepted. However, if a packet doesn't match any rule, it arrives at the last rule in the Iptables rules chain with the highest order. To make sure that this policy is the last policy in the chain, use a much higher order, such as <code>3000</code>, than the policy you created in step 1.</td>
   </tr>
  </tbody>
  </table>

3. Apply the policy.
  ```
  calicoctl apply -f log-denied-packets.yaml --config=<filepath>/calicoctl.cfg
  ```
  {: pre}

4. Generate log entries by sending requests that are not allowed by the policy that you created in step 1. For example, try to ping the pod that is protected by the network policy from a pod or an IP address that is not permitted.

5. Check for log entries that are written to the `/var/log/syslog` path. The DST (destination) or SRC (source) IP addresses in the log entry might be different than expected due to proxies, Network Address Translation (NAT), and other networking processes. The log entry looks similar to the following.
  ```
  Sep 5 14:34:40 <worker_hostname> kernel: [158271.044316] calico-packet: IN=eth1 OUT= MAC=08:00:27:d5:4e:57:0a:00:27:00:00:00:08:00 SRC=192.XXX.XX.X DST=192.XXX.XX.XX LEN=60 TOS=0x00 PREC=0x00 TTL=64 ID=52866 DF PROTO=TCP SPT=42962 DPT=22 WINDOW=29200 RES=0x00 SYN URGP=0
  ```
  {: screen}

6. Optional: [Forward the logs](/docs/containers?topic=containers-health#configuring) from `/var/log/syslog` to an external syslog server.



