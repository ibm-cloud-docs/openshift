---

copyright:
  years: 2014, 2019
lastupdated: "2019-10-30"

keywords: openshift, roks, rhos, rhoks, strongswan, ipsec, on-prem

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

# Setting up VPN connectivity
{: #vpn}



With VPN connectivity, you can securely connect apps in a OpenShift cluster on {{site.data.keyword.openshiftlong}} to an on-premises network. You can also connect apps that are external to your cluster to an app that runs inside your cluster.
{:shortdesc}

To connect your worker nodes and apps to an on-premises data center, you can configure one of the following options.

- **strongSwan IPSec VPN Service**: You can set up a [strongSwan IPSec VPN service ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.strongswan.org/about.html) that securely connects your OpenShift cluster with an on-premises network. The strongSwan IPSec VPN service provides a secure end-to-end communication channel over the internet that is based on the industry-standard Internet Protocol Security (IPSec) protocol suite. To set up a secure connection between your cluster and an on-premises network, [configure and deploy the strongSwan IPSec VPN service](#vpn-setup) directly in a pod in your cluster.

- **{{site.data.keyword.BluDirectLink}}**: [{{site.data.keyword.cloud_notm}} Direct Link](/docs/infrastructure/direct-link?topic=direct-link-about-ibm-cloud-direct-link) allows you to create a direct, private connection between your remote network environments and {{site.data.keyword.containerlong_notm}} without routing over the public internet. The {{site.data.keyword.cloud_notm}} Direct Link offerings are useful when you must implement hybrid workloads, cross-provider workloads, large or frequent data transfers, or private workloads. To choose an {{site.data.keyword.cloud_notm}} Direct Link offering and set up an {{site.data.keyword.cloud_notm}} Direct Link connection, see [Get Started with IBM Cloud {{site.data.keyword.cloud_notm}} Direct Link](/docs/infrastructure/direct-link?topic=direct-link-get-started-with-ibm-cloud-direct-link#how-do-i-know-which-type-of-ibm-cloud-direct-link-i-need-) in the {{site.data.keyword.cloud_notm}} Direct Link documentation.

- **Virtual Router Appliance (VRA) or Fortigate Security Appliance (FSA)**: You might choose to set up a [VRA (Vyatta)](/docs/infrastructure/virtual-router-appliance?topic=virtual-router-appliance-about-the-vra) or [FSA](/docs/services/vmwaresolutions/services?topic=vmware-solutions-fsa_considerations) to configure an IPSec VPN endpoint. This option is useful when you have a larger cluster, want to access multiple clusters over a single VPN, or need a route-based VPN. To configure a VRA, see [Setting up VPN connectivity with VRA](#vyatta).

## Using the strongSwan IPSec VPN service Helm chart
{: #vpn-setup}

Use a Helm chart to configure and deploy the strongSwan IPSec VPN service inside of a Kubernetes pod.
{:shortdesc}

Because strongSwan is integrated within your cluster, you don't need an external gateway appliance. When VPN connectivity is established, routes are automatically configured on all of the worker nodes in the cluster. These routes allow two-way connectivity through the VPN tunnel between pods on any worker node and the remote system. For example, the following diagram shows how an app in {{site.data.keyword.containerlong_notm}} can communicate with an on-premises server via a strongSwan VPN connection:

<img src="images/cs_vpn_strongswan.png" width="700" alt="Flow of traffic between your cluster and an on-premises data center through the strongSwan VPN service" style="width:700px; border-style: none"/>

1. An app in your cluster, `myapp`, receives a request from an Ingress or LoadBalancer service and needs to securely connect to data in your on-premises network.

2. The request to the on-premises data center is forwarded to the IPSec strongSwan VPN pod. The destination IP address is used to determine which network packets to send to the IPSec strongSwan VPN pod.

3. The request is encrypted and sent over the VPN tunnel to the on-premises data center.

4. The incoming request passes through the on-premises firewall and is delivered to the VPN tunnel endpoint (router) where it is decrypted.

5. The VPN tunnel endpoint (router) forwards the request to the on-premises server or mainframe, depending on the destination IP address that was specified in step 2. The necessary data is sent back over the VPN connection to `myapp` through the same process.

## strongSwan VPN service considerations
{: #strongswan_limitations}

Before using the strongSwan Helm chart, review the following considerations and limitations.
{: shortdesc}

* The strongSwan Helm chart requires NAT traversal to be enabled by the remote VPN endpoint. NAT traversal requires UDP port 4500 in addition to the default IPSec UDP port of 500. Both UDP ports need to be allowed through any firewall that is configured.
* The strongSwan Helm chart does not support route-based IPSec VPNs.
* The strongSwan Helm chart supports IPSec VPNs that use preshared keys, but does not support IPSec VPNs that require certificates.
* The strongSwan Helm chart does not allow multiple clusters and other IaaS resources to share a single VPN connection.
* The strongSwan Helm chart runs as a Kubernetes pod inside of the cluster. The VPN performance is affected by the memory and network usage of Kubernetes and other pods that are running in the cluster. If you have a performance-critical environment, consider using a VPN solution that runs outside of the cluster on dedicated hardware.
* The strongSwan Helm chart runs a single VPN pod as the IPSec tunnel endpoint. If the pod fails, the cluster restarts the pod. However, you might experience a short down time while the new pod starts and the VPN connection is re-established. If you require faster error recovery or a more elaborate high availability solution, consider using a VPN solution that runs outside of the cluster on dedicated hardware.
* The strongSwan Helm chart does not provide metrics or monitoring of the network traffic flowing over the VPN connection. For a list of supported monitoring tools, see [Logging and monitoring services](/docs/containers?topic=containers-supported_integrations#health_services).

Your cluster users can use the strongSwan VPN service to connect to your Kubernetes master through the private service endpoint. However, communication with the Kubernetes master over the private service endpoint must go through the <code>166.X.X.X</code> IP address range, which is not routable from a VPN connection. You can expose the private service endpoint of the master for your cluster users by [using a private network load balancer (NLB)](/docs/containers?topic=containers-clusters#access_on_prem). The private NLB exposes the private service endpoint of the master as an internal `172.21.x.x` cluster IP address that the strongSwan VPN pod can access. If you enable only the private service endpoint, you can use the Kubernetes dashboard or temporarily enable the public service endpoint to create the private NLB.
{: tip}

<br />


## Configuring the strongSwan VPN in a multizone cluster
{: #vpn_multizone}

Multizone clusters provide high availability for apps in the event of an outage by making app instances available on worker nodes in multiple zones. However, configuring the strongSwan VPN service in a multizone cluster is more complex than configuring strongSwan in a single-zone cluster.
{: shortdesc}

Before you configure strongSwan in a multizone cluster, first try to deploy a strongSwan Helm chart into a single-zone cluster. When you first establish a VPN connection between a single-zone cluster and an on-premises network, you can more easily determine remote network firewall settings that are important for a multizone strongSwan configuration:
* Some remote VPN endpoints have settings such as `leftid` or `rightid` in the `ipsec.conf` file. If you have these settings, check whether you must set the `leftid` to the IP address of the VPN IPSec tunnel.
*	If the connection is inbound to the cluster from the remote network, check whether the remote VPN endpoint can re-establish the VPN connection to a different IP address in case of load balancer failure in one zone.

To get started with strongSwan in a multizone cluster, choose one of the following options.
* If you can use an outbound VPN connection, you can choose to configure only one strongSwan VPN deployment. See [Configuring one outbound VPN connection from a multizone cluster](#multizone_one_outbound).
* If you require an inbound VPN connection, the configuration settings you can use vary depending on whether the remote VPN endpoint can be configured to re-establish the VPN connection to a different public load balancer IP when an outage is detected.
  * If the remote VPN endpoint can automatically re-establish the VPN connection to a different IP, you can choose to configure only one strongSwan VPN deployment. See [Configuring one inbound VPN connection to a multizone cluster](#multizone_one_inbound).
  * If the remote VPN endpoint cannot automatically re-establish the VPN connection to a different IP, you must deploy a separate inbound strongSwan VPN service in each zone. See [Configuring a VPN connection in each zone of a multizone cluster](#multizone_multiple).

Try to set up your environment so that you need only one strongSwan VPN deployment for an outbound or inbound VPN connection to your multizone cluster. If you must set up separate strongSwan VPNs in each zone, make sure that you plan how to manage this added complexity and increased resource usage.
{: note}

### Configuring a single outbound VPN connection from a multizone cluster
{: #multizone_one_outbound}

The simplest solution for configuring the strongSwan VPN service in a multizone cluster is to use a single outbound VPN connection that floats between different worker nodes across all availability zones in your cluster.
{: shortdesc}

When the VPN connection is outbound from the multizone cluster, only one strongSwan deployment is required. If a worker node is removed or experiences downtime, `kubelet` reschedules the VPN pod onto a new worker node. If an availability zone experiences an outage, `kubelet` reschedules the VPN pod onto a new worker node in a different zone.

1. [Configure one strongSwan VPN Helm chart](/docs/openshift?topic=openshift-vpn#vpn_configure). When you follow the steps in that section, ensure that you specify the following settings:
    - `ipsec.auto`: Change to `start`. Connections are outbound from the cluster.
    - `loadBalancerIP`: Do not specify an IP address. Leave this setting blank.
    - `zoneLoadBalancer`: Specify a public load balancer IP address for each zone where you have worker nodes. [You can check to see your available public IP addresses](/docs/openshift?topic=openshift-subnets#review_ip) or [free up a used IP address](/docs/openshift?topic=openshift-subnets#free). Because the strongSwan VPN pod can be scheduled to a worker node in any zone, this list of IPs ensures that a load balancer IP can be used in any zone where the VPN pod is scheduled.
    - `connectUsingLoadBalancerIP`: Set to `true`. When the strongSwan VPN pod is scheduled onto a worker node, the strongSwan service selects the load balancer IP address that is in the same zone and uses this IP to establish the outbound connection.
    - `local.id`: Specify a fixed value that is supported by your remote VPN endpoint. If the remote VPN endpoint requires you to set the `local.id` option (`leftid` value in `ipsec.conf`) to the public IP address of the VPN IPSec tunnel, set `local.id` to `%loadBalancerIP`. This value automatically configures the `leftid` value in `ipsec.conf` to the load balancer IP address that is used for the connection.
    - Optional: Hide all of the cluster IP addresses behind a single IP address in each zone by setting `enableSingleSourceIP` to `true`. This option provides one of the most secure configurations for the VPN connection because no connections from the remote network back into the cluster are permitted. You must also set `local.subnet` to the `%zoneSubnet` variable, and use the `local.zoneSubnet` to specify an IP address as a /32 subnet for each zone of the cluster.

2. In your remote network firewall, allow incoming IPSec VPN connections from the public IP addresses you listed in the `zoneLoadBalancer` setting.

3. Configure the remote VPN endpoint to allow an incoming VPN connection from each of the possible load balancer IPs that you listed in the `zoneLoadBalancer` setting.

### Configuring a single inbound VPN connection to a multizone cluster
{: #multizone_one_inbound}

When you require incoming VPN connections and the remote VPN endpoint can automatically re-establish the VPN connection to a different IP when a failure is detected, you can use a single inbound VPN connection that floats between different worker nodes across all availability zones in your cluster.
{: shortdesc}

The remote VPN endpoint can establish the VPN connection to any of the strongSwan load balancers in any of the zones. The incoming request is sent to the VPN pod regardless of which zone the VPN pod is in. Responses from the VPN pod are sent back through the original load balancer to the remote VPN endpoint. This option ensures high availability because `kubelet` reschedules the VPN pod onto a new worker node if a worker node is removed or experiences downtime. Additionally, if an availability zone experiences an outage, the remote VPN endpoint can re-establish the VPN connection to the load balancer IP address in a different zone so that the VPN pod can still be reached.

1. [Configure one strongSwan VPN Helm chart](/docs/openshift?topic=openshift-vpn#vpn_configure). When you follow the steps in that section, ensure that you specify the following settings:
    - `ipsec.auto`: Change to `add`. Connections are inbound to the cluster.
    - `loadBalancerIP`: Do not specify an IP address. Leave this setting blank.
    - `zoneLoadBalancer`: Specify a public load balancer IP address for each zone where you have worker nodes. [You can check to see your available public IP addresses](/docs/openshift?topic=openshift-subnets#review_ip) or [free up a used IP address](/docs/openshift?topic=openshift-subnets#free).
    - `local.id`: If the remote VPN endpoint requires you to set the `local.id` option (`leftid` value in `ipsec.conf`) to the public IP address of the VPN IPSec tunnel, set `local.id` to `%loadBalancerIP`. This value automatically configures the `leftid` value in `ipsec.conf` to the load balancer IP address that is used for the connection.

2. In your remote network firewall, allow outgoing IPSec VPN connections to the public IP addresses you listed in the `zoneLoadBalancer` setting.

### Configuring an inbound VPN connection in each zone of a multizone cluster
{: #multizone_multiple}

When you require incoming VPN connections and the remote VPN endpoint cannot re-establish the VPN connection to a different IP, you must deploy a separate strongSwan VPN service in each zone.
{: shortdesc}

The remote VPN endpoint must be updated to establish a separate VPN connection to a load balancer in each of the zones. Additionally, you must configure zone-specific settings on the remote VPN endpoint so that each of these VPN connections is unique. Ensure that these multiple incoming VPN connections remain active at all times.

After you deploy each Helm chart, each strongSwan VPN deployment starts up as a Kubernetes load balancer service in the correct zone. Incoming requests to that public IP are forwarded to the VPN pod that is also allocated in the same zone. If the zone experiences an outage, the VPN connections that are established in the other zones are unaffected.

1. [Configure a strongSwan VPN Helm chart](/docs/openshift?topic=openshift-vpn#vpn_configure) for each zone. When you follow the steps in that section, ensure that you specify the following settings:
    - `loadBalancerIP`: Specify an available public load balancer IP address that is in the zone where you deploy this strongSwan service. [You can check to see your available public IP addresses](/docs/openshift?topic=openshift-subnets#review_ip) or [free up a used IP address](/docs/openshift?topic=openshift-subnets#free).
    - `zoneSelector`: Specify the zone where you want the VPN pod to be scheduled.
    - Additional settings, such as `zoneSpecificRoutes`, `remoteSubnetNAT`, `localSubnetNAT`, or `enableSingleSourceIP`, might be required depending on which resources must be accessible over the VPN. See the next step for more details.

2. Configure zone-specific settings on both sides of the VPN tunnel to ensure that each VPN connection is unique. Depending on which resources must be accessible over the VPN, you have two options for making the connections distinguishable:
    * If pods in the cluster must access services on the remote on-premises network:
      - `zoneSpecificRoutes`: Set to `true`. This setting restricts the VPN connection to a single zone in the cluster. Pods in a specific zone use only the VPN connection that is set up for that specific zone. This solution reduces the number of strongSwan pods that are required to support multiple VPNs in a multizone cluster, improves VPN performance because the VPN traffic only flows to worker nodes located in the current zone, and ensures that VPN connectivity for each zone is unaffected by VPN connectivity, crashed pods, or zone outages in other zones. Note that you do not need to configure `remoteSubnetNAT`. Multiple VPNs that use the `zoneSpecificRoutes` setting can have the same `remote.subnet` because the routing is setup on a per-zone basis.
      - `enableSingleSourceIP`: Set to `true` and set the `local.subnet` to a single /32 IP address. This combination of settings hides all of the cluster private IP addresses behind a single /32 IP address. This unique /32 IP address allows the remote on-premises network to send replies back over the correct VPN connection to the correct pod in the cluster that initiated the request. Note that the single /32 IP address that is configured for the `local.subnet` option must be unique in each strongSwan VPN configuration.
    * If applications in the remote on-premises network must access services in the cluster:
      - `localSubnetNAT`: Ensure that an application in the on-premises remote network can select a specific VPN connection to send and receive traffic to the cluster. In each strongSwan Helm configuration, use `localSubnetNAT` to uniquely identify the cluster resources that can be accessed by the remote on-premises application. Because multiple VPNs are established from the remote on-premises network to the cluster, you must add logic to the application on the on-premise network so that it can select which VPN to use when it accesses services in the cluster. Note that the services in the cluster are accessible through multiple different subnets depending on what you configured for `localSubnetNAT` in each strongSwan VPN configuration.
      - `remoteSubnetNAT`: Ensure that a pod in your cluster uses the same VPN connection to return traffic to the remote network. In each strongSwan deployment file, map the remote on-premises subnet to a unique subnet using the `remoteSubnetNAT` setting. Traffic that is received by a pod in the cluster from a VPN-specific `remoteSubnetNAT` is sent back to that same VPN-specific `remoteSubnetNAT` and then over that same VPN connection.

3. Configure the remote VPN endpoint software to establish a separate VPN connection to the load balancer IP in each zone.

<br />


## Configuring the strongSwan Helm chart
{: #vpn_configure}

Before you install the strongSwan Helm chart, you must decide on your strongSwan configuration.
{: shortdesc}

Before you begin:
* Install an IPSec VPN gateway in your on-premises data center.
* Ensure you have the [**Writer** or **Manager** {{site.data.keyword.cloud_notm}} IAM service role](/docs/openshift?topic=openshift-users#platform) for the `default` namespace.
* [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)
  * **Note**: All strongSwan configurations are permitted in standard clusters. If you use a free cluster, you can choose only an outbound VPN connection in [Step 3](#strongswan_3). Inbound VPN connections require a load balancer in the cluster, and load balancers are not available for free clusters.

### Step 1: Get the strongSwan Helm chart
{: #strongswan_1}

Install Helm and get the strongSwan Helm chart to view possible configurations.
{: shortdesc}

1.  [Follow the instructions](/docs/containers?topic=containers-helm#public_helm_install) to install the Helm client on your local machine, install the Helm server (tiller) with a service account, and add the {{site.data.keyword.cloud_notm}} Helm repository. Note that Helm version 2.8 or later is required.

2.  Verify that tiller is installed with a service account.

    ```
    oc get serviceaccount -n kube-system | grep tiller
    ```
    {: pre}

    Example output:

    ```
    NAME                                 SECRETS   AGE
    tiller                               1         2m
    ```
    {: screen}

3. Save the default configuration settings for the strongSwan Helm chart in a local YAML file.

    ```
    helm inspect values iks-charts/strongswan > config.yaml
    ```
    {: pre}

4. Open the `config.yaml` file.

### Step 2: Configure basic IPSec settings
{: #strongswan_2}

To control the establishment of the VPN connection, modify the following basic IPSec settings.
{: shortdesc}

For more information about each setting, read the documentation provided within the `config.yaml` file for the Helm chart.
{: tip}

1. If your on-premises VPN tunnel endpoint does not support `ikev2` as a protocol for initializing the connection, change the value of `ipsec.keyexchange` to `ikev1`.
2. Set `ipsec.esp` to a list of ESP encryption and authentication algorithms that your on-premises VPN tunnel endpoint uses for the connection.
    * If `ipsec.keyexchange` is set to `ikev1`, this setting must be specified.
    * If `ipsec.keyexchange` is set to `ikev2`, this setting is optional.
    * If you leave this setting blank, the default strongSwan algorithms `aes128-sha1,3des-sha1` are used for the connection.
3. Set `ipsec.ike` to a list of IKE/ISAKMP SA encryption and authentication algorithms that your on-premises VPN tunnel endpoint uses for the connection. The algorithms must be specific in the format `encryption-integrity[-prf]-dhgroup`.
    * If `ipsec.keyexchange` is set to `ikev1`, this setting must be specified.
    * If `ipsec.keyexchange` is set to `ikev2`, this setting is optional.
    * If you leave this setting blank, the default strongSwan algorithms `aes128-sha1-modp2048,3des-sha1-modp1536` are used for the connection.
4. Change the value of `local.id` to any string that you want to use to identify the local OpenShift cluster side that your VPN tunnel endpoint uses. The default is `ibm-cloud`. Some VPN implementations require that you use the public IP address for the local endpoint.
5. Change the value of `remote.id` to any string that you want to use to identify the remote on-premises side that your VPN tunnel endpoint uses. The default is `on-prem`. Some VPN implementations require that you use the public IP address for the remote endpoint.
6. Change the value of `preshared.secret` to the pre-shared secret that your on-premises VPN tunnel endpoint gateway uses for the connection. This value is stored in `ipsec.secrets`.
7. Optional: Set `remote.privateIPtoPing` to any private IP address in the remote subnet to ping as part of the Helm connectivity validation test.

### Step 3: Select inbound or outbound VPN connection
{: #strongswan_3}

When you configure a strongSwan VPN connection, you choose whether the VPN connection is inbound to the cluster or outbound from the cluster.
{: shortdesc}

<dl>
<dt>Inbound</dt>
<dd>The on-premises VPN endpoint from the remote network initiates the VPN connection, and the cluster listens for the connection.</dd>
<dt>Outbound</dt>
<dd>The cluster initiates the VPN connection, and the on-premises VPN endpoint from the remote network listens for the connection.</dd>
</dl>

If you use a free cluster, you can choose only an outbound VPN connection. Inbound VPN connections require a load balancer in the cluster, and load balancers are not available for free clusters.

To establish an inbound VPN connection, modify the following settings:
1. Verify that `ipsec.auto` is set to `add`.
2. Optional: Set `loadBalancerIP` to a portable public IP address for the strongSwan VPN service. Specifying an IP address is useful when you need a stable IP address, such as when you must designate which IP addresses are permitted through an on-premises firewall. The cluster must have at least one available public load balancer IP address. [You can check to see your available public IP addresses](/docs/openshift?topic=openshift-subnets#review_ip) or [free up a used IP address](/docs/openshift?topic=openshift-subnets#free).
    * If you leave this setting blank, one of the available portable public IP addresses is used.
    * You must also configure the public IP address that you select for or the public IP address that is assigned to the cluster VPN endpoint on the on-premises VPN endpoint.

To establish an outbound VPN connection, modify the following settings:
1. Change `ipsec.auto` to `start`.
2. Set `remote.gateway` to the public IP address for the on-premises VPN endpoint in the remote network.
3. Choose one of the following options for the IP address for the cluster VPN endpoint:
    * **Public IP address of the cluster's private gateway**: If your worker nodes are connected to a private VLAN only, then the outbound VPN request is routed through the private gateway in order to reach the internet. The public IP address of the private gateway is used for the VPN connection.
    * **Public IP address of the worker node where the strongSwan pod runs**: If the worker node where the strongSwan pod runs is connected to a public VLAN, then the worker node's public IP address is used for the VPN connection.
        <br>
        * If the strongSwan pod is deleted and rescheduled onto a different worker node in the cluster, then the public IP address of the VPN changes. The on-premises VPN endpoint of the remote network must allow the VPN connection to be established from the public IP address of any of the cluster worker nodes.
        * If the remote VPN endpoint cannot handle VPN connections from multiple public IP addresses, limit the nodes that the strongSwan VPN pod deploys to. Set `nodeSelector` to the IP addresses of specific worker nodes or a worker node label. For example, the value `kubernetes.io/hostname: 10.232.xx.xx` allows the VPN pod to deploy to that worker node only. The value `strongswan: vpn` restricts the VPN pod to running on any worker nodes with that label. You can use any worker node label. To allow different worker nodes to be used with different helm chart deployments, use `strongswan: <release_name>`. For high availability, select at least two worker nodes.
    * **Public IP address of the strongSwan service**: To establish connection by using the IP address of the strongSwan VPN service, set `connectUsingLoadBalancerIP` to `true`. The strongSwan service IP address is either a portable public IP address you can specify in the `loadBalancerIP` setting, or an available portable public IP address that is automatically assigned to the service.
        <br>
        * If you choose to select an IP address using the `loadBalancerIP` setting, the cluster must have at least one available public load balancer IP address. [You can check to see your available public IP addresses](/docs/openshift?topic=openshift-subnets#review_ip) or [free up a used IP address](/docs/openshift?topic=openshift-subnets#free).
        * All of the cluster worker nodes must be on the same public VLAN. Otherwise, you must use the `nodeSelector` setting to ensure that the VPN pod deploys to a worker node on the same public VLAN as the `loadBalancerIP`.
        * If `connectUsingLoadBalancerIP` is set to `true` and `ipsec.keyexchange` is set to `ikev1`, you must set `enableServiceSourceIP` to `true`.

### Step 4: Access cluster resources over the VPN connection
{: #strongswan_4}

Determine which cluster resources must be accessible by the remote network over the VPN connection.
{: shortdesc}

1. Add the CIDRs of one or more cluster subnets to the `local.subnet` setting. You must configure the local subnet CIDRs on the on-premises VPN endpoint. This list can include the following subnets:
    * The Kubernetes pod subnet CIDR: `172.30.0.0/16`. Bidirectional communication is enabled between all cluster pods and any of the hosts in the remote network subnets that you list in the `remote.subnet` setting. If you must prevent any `remote.subnet` hosts from accessing cluster pods for security reasons, do not add the Kubernetes pod subnet to the `local.subnet` setting.
    * The Kubernetes service subnet CIDR: `172.21.0.0/16`. Service IP addresses provide a way to expose multiple app pods that are deployed on several worker nodes behind a single IP.
    * If your apps are exposed by a NodePort service on the private network or a private Ingress ALB, add the worker node's private subnet CIDR. Retrieve the first three octets of your worker's private IP address by running `ibmcloud oc worker <cluster_name>`. For example, if it is `10.176.48.xx` then note `10.176.48`. Next, get the worker private subnet CIDR by running the following command, replacing `<xxx.yyy.zz>` with the octet that you previously retrieved: `ibmcloud sl subnet list | grep <xxx.yyy.zzz>`. **Note**: If a worker node is added on a new private subnet, you must add the new private subnet CIDR to the `local.subnet` setting and the on-premises VPN endpoint. Then, the VPN connection must be restarted.
    * If you have apps that are exposed by LoadBalancer services on the private network, add the cluster's private user-managed subnet CIDRs. To find these values, run `ibmcloud oc cluster get --cluster <cluster_name> --show-resources`. In the **VLANs** section, look for CIDRs that have a **Public** value of `false`. **Note**: If `ipsec.keyexchange` is set to `ikev1`, you can specify only one subnet. However, you can use the `localSubnetNAT` setting to combine multiple cluster subnets into a single subnet.

2. Optional: Remap cluster subnets by using the `localSubnetNAT` setting. Network Address Translation (NAT) for subnets provides a workaround for subnet conflicts between the cluster network and on-premises remote network. You can use NAT to remap the cluster's private local IP subnets, the pod subnet (172.30.0.0/16), or the pod service subnet (172.21.0.0/16) to a different private subnet. The VPN tunnel sees remapped IP subnets instead of the original subnets. Remapping happens before the packets are sent over the VPN tunnel as well as after the packets arrive from the VPN tunnel. You can expose both remapped and non-remapped subnets at the same time over the VPN. To enable NAT, you can either add an entire subnet or individual IP addresses.
    * If you add an entire subnet in the format `10.171.42.0/24=10.10.10.0/24`, remapping is 1-to-1: all of the IP addresses in the internal network subnet are mapped over to external network subnet and vice versa.
    * If you add individual IP addresses in the format `10.171.42.17/32=10.10.10.2/32,10.171.42.29/32=10.10.10.3/32`, only those internal IP addresses are mapped to the specified external IP addresses.

3. Optional for version 2.2.0 and later strongSwan Helm charts: Hide all of the cluster IP addresses behind a single IP address by setting `enableSingleSourceIP` to `true`. This option provides one of the most secure configurations for the VPN connection because no connections from the remote network back into the cluster are permitted.
    <br>
    * This setting requires that all data flow over the VPN connection must be outbound regardless of whether the VPN connection is established from the cluster or from the remote network.
    * If you install strongSwan into a single-zone cluster, you must set `local.subnet` to only one IP address as a /32 subnet. If you install strongSwan in a multizone cluster, you can set `local.subnet` to the `%zoneSubnet` variable, and use the `local.zoneSubnet` to specify an IP address as a /32 subnet for each zone of the cluster.

4. Optional for version 2.2.0 and later strongSwan Helm charts: Enable the strongSwan service to route incoming requests from the remote network to a service that exists outside of the cluster by using the `localNonClusterSubnet` setting.
    <br>
    * The non-cluster service must exist on the same private network or on a private network that is reachable by the worker nodes.
    * The non-cluster worker node cannot initiate traffic to the remote network through the VPN connection, but the non-cluster node can be the target of incoming requests from the remote network.
    * You must list the CIDRs of the non-cluster subnets in the `local.subnet` setting.

### Step 5: Access remote network resources over the VPN connection
{: #strongswan_5}

Determine which remote network resources must be accessible by the cluster over the VPN connection.
{: shortdesc}

1. Add the CIDRs of one or more on-premises private subnets to the `remote.subnet` setting. **Note**: If `ipsec.keyexchange` is set to `ikev1`, you can specify only one subnet.
2. Optional for version 2.2.0 and later strongSwan Helm charts: Remap remote network subnets by using the `remoteSubnetNAT` setting. Network Address Translation (NAT) for subnets provides a workaround for subnet conflicts between the cluster network and on-premises remote network. You can use NAT to remap the remote network's IP subnets to a different private subnet. Remapping happens before the packets are sent over the VPN tunnel. Pods in the cluster see the remapped IP subnets instead of the original subnets. Before the pods send data back through the VPN tunnel, the remapped IP subnet is switched back to the actual subnet that is being used by the remote network. You can expose both remapped and non-remapped subnets at the same time over the VPN.

### Step 6 (optional): Enable monitoring with the Slack webhook integration
{: #strongswan_6}

To monitor the status of the strongSwan VPN, you can set up a webhook to automatically post VPN connectivity messages to a Slack channel.
{: shortdesc}

1. Sign in to your Slack workspace.

2. Go to the [Incoming WebHooks app page ![External link icon](../icons/launch-glyph.svg "External link icon")](https://slack.com/apps/A0F7XDUAZ-incoming-webhooks).

3. Click **Request to Install**. If this app is not listed in your Slack setup, contact your Slack workspace owner.

4. After your request to install is approved, click **Add Configuration**.

5. Choose a Slack channel or create a new channel to send the VPN messages to.

6. Copy the webhook URL that is generated. The URL format looks similar to the following:
  ```
  https://hooks.slack.com/services/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
  ```
  {: screen}

7. To verify that the Slack webhook is installed, send a test message to your webhook URL by running the following command:
    ```
    curl -X POST -H 'Content-type: application/json' -d '{"text":"VPN test message"}' <webhook_URL>
    ```
    {: pre}

8. Go to the Slack channel you chose to verify that the test message is successful.

9. In the `config.yaml` file for the Helm chart, configure the webhook to monitor your VPN connection.
    1. Change `monitoring.enable` to `true`.
    2. Add private IP addresses or HTTP endpoints in the remote subnet that you want ensure are reachable over the VPN connection to `monitoring.privateIPs` or `monitoring.httpEndpoints`. For example, you might add the IP from the `remote.privateIPtoPing` setting to `monitoring.privateIPs`.
    3. Add the webhook URL to `monitoring.slackWebhook`.
    4. Change other optional `monitoring` settings as needed.

### Step 7: Deploy the Helm chart
{: #strongswan_7}

Deploy the strongSwan Helm chart in your cluster with the configurations that you chose earlier.
{: shortdesc}

1. If you need to configure more advanced settings, follow the documentation provided for each setting in the Helm chart.

3. Save the updated `config.yaml` file.

4. Install the Helm chart to your cluster with the updated `config.yaml` file.

    If you have multiple VPN deployments in a single cluster, you can avoid naming conflicts and differentiate between your deployments by choosing more descriptive release names than `vpn`. To avoid the truncation of the release name, limit the release name to 35 characters or less.
    {: tip}

    ```
    helm install -f config.yaml --name=vpn iks-charts/strongswan
    ```
    {: pre}

5. Check the chart deployment status. When the chart is ready, the **STATUS** field near the top of the output has a value of `DEPLOYED`.

    ```
    helm status vpn
    ```
    {: pre}

6. Once the chart is deployed, verify that the updated settings in the `config.yaml` file were used.

    ```
    helm get values vpn
    ```
    {: pre}

## Testing and verifying strongSwan VPN connectivity
{: #vpn_test}

After you deploy your Helm chart, test the VPN connectivity.
{:shortdesc}

1. If the VPN on the on-premises gateway is not active, start the VPN.

2. Set the `STRONGSWAN_POD` environment variable.

    ```
    export STRONGSWAN_POD=$(oc get pod -l app=strongswan,release=vpn -o jsonpath='{ .items[0].metadata.name }')
    ```
    {: pre}

3. Check the status of the VPN. A status of `ESTABLISHED` means that the VPN connection was successful.

    ```
    oc exec $STRONGSWAN_POD -- ipsec status
    ```
    {: pre}

    Example output:

    ```
    Security Associations (1 up, 0 connecting):
    k8s-conn[1]: ESTABLISHED 17 minutes ago, 172.30.xxx.xxx[ibm-cloud]...192.xxx.xxx.xxx[on-premises]
    k8s-conn{2}: INSTALLED, TUNNEL, reqid 12, ESP in UDP SPIs: c78cb6b1_i c5d0d1c3_o
    k8s-conn{2}: 172.21.0.0/16 172.30.0.0/16 === 10.91.152.xxx/26
    ```
    {: screen}

    * When you try to establish VPN connectivity with the strongSwan Helm chart, it is likely that the VPN status is not `ESTABLISHED` the first time. You might need to check the on-premises VPN endpoint settings and change the configuration file several times before the connection is successful:
        1. Run `helm delete --purge <release_name>`
        2. Fix the incorrect values in the configuration file.
        3. Run `helm install -f config.yaml --name=<release_name> ibm/strongswan`
      You can also run more checks in the next step.

    * If the VPN pod is in an `ERROR` state or continues to crash and restart, it might be due to parameter validation of the `ipsec.conf` settings in the chart's configmap.
        1. Check for any validation errors in the strongSwan pod logs by running `oc logs $STRONGSWAN_POD`.
        2. If validation errors exist, run `helm delete --purge <release_name>`
        3. Fix the incorrect values in the configuration file.
        4. Run `helm install -f config.yaml --name=<release_name> ibm/strongswan`

4. You can further test the VPN connectivity by running the five Helm tests that are included in the strongSwan chart definition.

    ```
    helm test vpn
    ```
    {: pre}

    * If all of the tests pass, your strongSwan VPN connection is successfully set up.
    * If any of the tests fail, continue to the next step.

5. View the output of a failed test by looking at the logs of the test pod.

    ```
    oc logs <test_program>
    ```
    {: pre}

    Some of the tests have requirements that are optional settings in the VPN configuration. If some of the tests fail, the failures might be acceptable depending on whether you specified these optional settings. Refer to the following table for information about each test and why it might fail.
    {: note}

    {: #vpn_tests_table}
    <table>
    <caption>Understanding the Helm VPN connectivity tests</caption>
    <thead>
    <th colspan=2><img src="images/idea.png" alt="Idea icon"/> Understanding the Helm VPN connectivity tests</th>
    </thead>
    <tbody>
    <tr>
    <td><code>vpn-strongswan-check-config</code></td>
    <td>Validates the syntax of the <code>ipsec.conf</code> file that is generated from the <code>config.yaml</code> file. This test might fail due to incorrect values in the <code>config.yaml</code> file.</td>
    </tr>
    <tr>
    <td><code>vpn-strongswan-check-state</code></td>
    <td>Checks that the VPN connection has a status of <code>ESTABLISHED</code>. This test might fail for the following reasons:<ul><li>Differences between the values in the <code>config.yaml</code> file and the on-premises VPN endpoint settings.</li><li>If the cluster is in "listen" mode (<code>ipsec.auto</code> is set to <code>add</code>), the connection is not established on the on-premises side.</li></ul></td>
    </tr>
    <tr>
    <td><code>vpn-strongswan-ping-remote-gw</code></td>
    <td>Pings the <code>remote.gateway</code> public IP address that you configured in the <code>config.yaml</code> file. If the VPN connection has the <code>ESTABLISHED</code> status, you can ignore the result of this test. If the VPN connection does not have the <code>ESTABLISHED</code> status, this test might fail for the following reasons:<ul><li>You did not specify an on-premises VPN gateway IP address. If <code>ipsec.auto</code> is set to <code>start</code>, the <code>remote.gateway</code> IP address is required.</li><li>ICMP (ping) packets are being blocked by a firewall.</li></ul></td>
    </tr>
    <tr>
    <td><code>vpn-strongswan-ping-remote-ip-1</code></td>
    <td>Pings the <code>remote.privateIPtoPing</code> private IP address of the on-premises VPN gateway from the VPN pod in the cluster. This test might fail for the following reasons:<ul><li>You did not specify a <code>remote.privateIPtoPing</code> IP address. If you intentionally did not specify an IP address, this failure is acceptable.</li><li>You did not specify the cluster pod subnet CIDR, <code>172.30.0.0/16</code>, in the <code>local.subnet</code> list.</li></ul></td>
    </tr>
    <tr>
    <td><code>vpn-strongswan-ping-remote-ip-2</code></td>
    <td>Pings the <code>remote.privateIPtoPing</code> private IP address of the on-premises VPN gateway from the worker node in the cluster. This test might fail for the following reasons:<ul><li>You did not specify a <code>remote.privateIPtoPing</code> IP address. If you intentionally did not specify an IP address, this failure is acceptable.</li><li>You did not specify the cluster worker node private subnet CIDR in the <code>local.subnet</code> list.</li></ul></td>
    </tr>
    </tbody></table>

6. Delete the current Helm chart.

    ```
    helm delete --purge vpn
    ```
    {: pre}

7. Open the `config.yaml` file and fix the incorrect values.

8. Save the updated `config.yaml` file.

9. Install the Helm chart to your cluster with the updated `config.yaml` file. The updated properties are stored in a configmap for your chart.

    ```
    helm install -f config.yaml --name=<release_name> ibm/strongswan
    ```
    {: pre}

10. Check the chart deployment status. When the chart is ready, the **STATUS** field near the top of the output has a value of `DEPLOYED`.

    ```
    helm status vpn
    ```
    {: pre}

11. Once the chart is deployed, verify that the updated settings in the `config.yaml` file were used.

    ```
    helm get values vpn
    ```
    {: pre}

12. Clean up the current test pods.

    ```
    oc get pods -a -l app=strongswan-test
    ```
    {: pre}

    ```
    oc delete pods -l app=strongswan-test
    ```
    {: pre}

13. Run the tests again.

    ```
    helm test vpn
    ```
    {: pre}

<br />


## Limiting strongSwan VPN traffic by namespace or worker node
{: #limit}

If you have a single-tenant cluster, or if you have a multi-tenant cluster in which cluster resources are shared among the tenants, you can [limit VPN traffic for each strongSwan deployment to pods in certain namespaces](#limit_namespace). If you have a multi-tenant cluster in which cluster resources are dedicated to tenants, you can [limit VPN traffic for each strongSwan deployment to the worker nodes dedicated to each tenant](#limit_worker).
{: shortdesc}

### Limiting strongSwan VPN traffic by namespace
{: #limit_namespace}

When you have a single-tenant or multi-tenant cluster, you can limit VPN traffic to pods in only certain namespaces.
{: shortdesc}

For example, say that you want pods in only a specific namespace, `my-secure-namespace`, to send and receive data over the VPN. You do not want pods in other namespaces, such as `kube-system`, `ibm-system`, or `default`, to access your on-premises network. To limit the VPN traffic to only `my-secure-namespace`, you can create Calico global network policies.

Before you use this solution, review the following considerations and limitations.
* You do not need to deploy the strongSwan Helm chart into the specified namespace. The strongSwan VPN pod and the routes daemon set can be deployed into `kube-system` or any other namespace. If the strongSwan VPN is not deployed into the specified namespace, then the `vpn-strongswan-ping-remote-ip-1` Helm test fails. This failure is expected and acceptable. The test pings the `remote.privateIPtoPing` private IP address of the on-premises VPN gateway from a pod which is not in the namespace that has direct access to the remote subnet. However, the VPN pod is still able to forward traffic to pods in the namespaces that do have routes to the remote subnet, and traffic can still flow correctly. The VPN state is still `ESTABLISHED` and pods in the specified namespace can connect over the VPN.

* The Calico global network policies in the following steps do not prevent Kubernetes pods that use host networking from sending and receiving data over the VPN. When a pod is configured with host networking, the app running in the pod can listen on the network interfaces of the worker node that it is on. These host networking pods can exist in any namespace. To determine which pods have host networking, run `oc get pods --all-namespaces -o wide` and look for any pods that do not have a `172.30.0.0/16` pod IP address. If you want to prevent host networking pods from sending and receiving data over the VPN, you can set the following options in your `values.yaml` deployment file: `local.subnet: 172.30.0.0/16` and `enablePodSNAT: false`. These configuration settings expose all of the Kubernetes pods over the VPN connection to the remote network. However, only the pods that are located in the specified secure namespace are reachable over the VPN.

Before you begin:
* [Deploy the strongSwan Helm chart](#vpn_configure) and [ensure that VPN connectivity is working correctly](#vpn_test).
* [Install and configure the Calico CLI](/docs/openshift?topic=openshift-network_policies#cli_install).

To limit VPN traffic to a certain namespace:

1. Create a Calico global network policy named `allow-non-vpn-outbound.yaml`. This policy allows all namespaces to continue to send outbound traffic to all destinations, except to the remote subnet that the strongSwan VPN accesses. Replace `<remote.subnet>` with the `remote.subnet` that you specified in the Helm `values.yaml` configuration file. To specify multiple remote subnets, see the [Calico documentation ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.projectcalico.org/v3.3/reference/calicoctl/resources/globalnetworkpolicy).
    ```yaml
    apiVersion: projectcalico.org/v3
    kind: GlobalNetworkPolicy
    metadata:
      name: allow-non-vpn-outbound
    spec:
      selector: has(projectcalico.org/namespace)
      egress:
      - action: Allow
        destination:
          notNets:
          - <remote.subnet>
      order: 900
      types:
      - Egress
    ```
    {: codeblock}

2. Apply the policy.

    ```
    calicoctl apply -f allow-non-vpn-outbound.yaml --config=filepath/calicoctl.cfg
    ```
    {: pre}

3. Create another Calico global network policy named `allow-vpn-from-namespace.yaml`. This policy allows only a specified namespace to send outbound traffic to the remote subnet that the strongSwan VPN accesses. Replace `<namespace>` with the namespace that can access the VPN and `<remote.subnet>` with the `remote.subnet` that you specified in the Helm `values.yaml` configuration file. To specify multiple namespaces or remote subnets, see the [Calico documentation ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.projectcalico.org/v3.3/reference/calicoctl/resources/globalnetworkpolicy).
    ```yaml
    apiVersion: projectcalico.org/v3
    kind: GlobalNetworkPolicy
    metadata:
      name: allow-vpn-from-namespace
    spec:
      selector: projectcalico.org/namespace == "<namespace>"
      egress:
      - action: Allow
        destination:
          nets:
          - <remote.subnet>
      order: 900
      types:
      - Egress
    ```
    {: codeblock}

4. Apply the policy.

    ```
    calicoctl apply -f allow-vpn-from-namespace.yaml --config=filepath/calicoctl.cfg
    ```
    {: pre}

5. Verify that the global network policies are created in your cluster.
    ```
    calicoctl get GlobalNetworkPolicy -o wide --config=filepath/calicoctl.cfg
    ```
    {: pre}

### Limiting strongSwan VPN traffic by worker node
{: #limit_worker}

When you have multiple strongSwan VPN deployments in a multi-tenant cluster, you can limit VPN traffic for each deployment to specific worker nodes that are dedicated to each tenant.
{: shortdesc}

When you deploy a strongSwan Helm chart, a strongSwan VPN deployment is created. The strongSwan VPN pods are deployed to any untainted worker nodes. Additionally, a Kubernetes daemon set is created. This daemon set automatically configures routes on all untainted worker nodes in the cluster to each of the remote subnets. The strongSwan VPN pod uses the routes on worker nodes to forward requests to the remote subnet in the on-premises network.

Routes are not configured on tainted nodes unless you specify the taint in the `tolerations` setting in the `value.yaml` file. By tainting worker nodes, you can prevent any VPN routes from being configured on those workers. Then, you can specify the taint in the `tolerations` setting for only the VPN deployment that you do want to permit on the tainted workers. In this way, the strongSwan VPN pods for one tenant's Helm chart deployment only use the routes on that tenant's worker nodes to forward traffic over the VPN connection to the remote subnet.

Before you use this solution, review the following considerations and limitations.
* By default, Kubernetes places app pods onto any untainted worker nodes that are available. To make sure that this solution works correctly, each tenant must first ensure that they deploy their app pods only to workers that are tainted for the correct tenant. Additionally, each tainted worker node must also have a toleration to allow the app pods to be placed on the node. For more information about taints and tolerations, see the [Kubernetes documentation ![External link icon](../icons/launch-glyph.svg "External link icon")](https://kubernetes.io/docs/concepts/configuration/taint-and-toleration/).
* Cluster resources might not be optimally utilized because neither tenant can place app pods on the shared non-tainted nodes.

The following steps for limiting strongSwan VPN traffic by worker node use this example scenario: Say that you have a multi-tenant {{site.data.keyword.containerlong_notm}} cluster with six worker nodes. The cluster supports tenant A and tenant B. You taint the worker nodes in the following ways:
* Two worker nodes are tainted so that only tenant A pods are scheduled on the workers.
* Two worker nodes are tainted so that only tenant B pods are scheduled on the workers.
* Two worker nodes are not tainted because at least 2 worker nodes are required for the strongSwan VPN pods and the load balancer IP to run on.

To limit VPN traffic to tainted nodes for each tenant:

1. To limit the VPN traffic to only workers dedicated to tenant A in this example, you specify the following `toleration` in the `values.yaml` file for the tenant A strongSwan Helm chart:
    ```
    tolerations:
     - key: dedicated
       operator: "Equal"
       value: "tenantA"
       effect: "NoSchedule"
    ```
    {: codeblock}
    This toleration allows the route daemon set to run on the two worker nodes that have the `dedicated="tenantA"` taint and on the two untainted worker nodes. The strongSwan VPN pods for this deployment run on the two untainted worker nodes.

2. To limit the VPN traffic to only workers dedicated to tenant B in this example, you specify the following `toleration` in the `values.yaml` file for the tenant B strongSwan Helm chart:
    ```
    tolerations:
     - key: dedicated
       operator: "Equal"
       value: "tenantB"
       effect: "NoSchedule"
    ```
    {: codeblock}
    This toleration allows the route daemon set to run on the two worker nodes that have the `dedicated="tenantB"` taint and on the two untainted worker nodes. The strongSwan VPN pods for this deployment also run on the two untainted worker nodes.

<br />


## Upgrading or disabling the strongSwan Helm chart
{: #vpn_upgrade}

Make sure your strongSwan Helm chart is up-to-date by upgrading it.
{:shortdesc}

To upgrade your strongSwan Helm chart to the latest version:

  ```
  helm upgrade -f config.yaml <release_name> ibm/strongswan
  ```
  {: pre}

You can disable the VPN connection by deleting the Helm chart.

  ```
  helm delete --purge <release_name>
  ```
  {: pre}

<br />


## Using a Virtual Router Appliance
{: #vyatta}

The [Virtual Router Appliance (VRA)](/docs/infrastructure/virtual-router-appliance?topic=virtual-router-appliance-about-the-vra) provides the latest Vyatta 5600 operating system for x86 bare metal servers. You can use a VRA as VPN gateway to securely connect to an on-premises network.
{:shortdesc}

All public and private network traffic that enters or exits the cluster VLANs is routed through a VRA. You can use the VRA as a VPN endpoint to create an encrypted IPSec tunnel between servers in IBM Cloud infrastructure and on-premises resources. For example, the following diagram shows how an app on a private-only worker node in {{site.data.keyword.containerlong_notm}} can communicate with an on-premises server via a VRA VPN connection:

<img src="images/cs_vpn_vyatta.png" width="725" alt="Expose an app in {{site.data.keyword.containerlong_notm}} by using a load balancer" style="width:725px; border-style: none"/>

1. An app in your cluster, `myapp2`, receives a request from an Ingress or LoadBalancer service and needs to securely connect to data in your on-premises network.

2. Because `myapp2` is on a worker node that is on a private VLAN only, the VRA acts as a secure connection between the worker nodes and the on-premises network. The VRA uses the destination IP address to determine which network packets to send to the on-premises network.

3. The request is encrypted and sent over the VPN tunnel to the on-premises data center.

4. The incoming request passes through the on-premises firewall and is delivered to the VPN tunnel endpoint (router) where it is decrypted.

5. The VPN tunnel endpoint (router) forwards the request to the on-premises server or mainframe, depending on the destination IP address that was specified in step 2. The necessary data is sent back over the VPN connection to `myapp2` through the same process.

To set up a Virtual Router Appliance:

1. [Order a VRA](/docs/infrastructure/virtual-router-appliance?topic=virtual-router-appliance-getting-started).

2. [Configure the private VLAN on the VRA](/docs/infrastructure/virtual-router-appliance?topic=gateway-appliance-managing-vlans-and-gateway-appliances).

3. To enable a VPN connection by using the VRA, [configure VRRP on the VRA](/docs/infrastructure/virtual-router-appliance?topic=virtual-router-appliance-working-with-high-availability-and-vrrp#high-availability-vpn-with-vrrp).

If you have an existing router appliance and then add a cluster, the new portable subnets that are ordered for the cluster are not configured on the router appliance. In order to use networking services, you must enable routing between the subnets on the same VLAN by [enabling VLAN spanning](/docs/openshift?topic=openshift-subnets#subnet-routing). To check if VLAN spanning is already enabled, use the `ibmcloud oc vlan spanning get --region <region>` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_vlan_spanning_get).
{: important}

