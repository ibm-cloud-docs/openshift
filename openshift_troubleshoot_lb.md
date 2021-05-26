---

copyright:
  years: 2014, 2021
lastupdated: "2021-05-26"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift
content-type: troubleshoot

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:api: .ph data-hd-interface='api'}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
{:codeblock: .codeblock}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:fuzzybunny: .ph data-hd-programlang='fuzzybunny'}
{:generic: data-hd-operatingsystem="generic"}
{:generic: data-hd-programlang="generic"}
{:gif: data-image-type='gif'}
{:go: .ph data-hd-programlang='go'}
{:help: data-hd-content-type='help'}
{:hide-dashboard: .hide-dashboard}
{:hide-in-docs: .hide-in-docs}
{:important: .important}
{:ios: data-hd-operatingsystem="ios"}
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:new_window: target="_blank"}
{:note .note}
{:note: .note}
{:objectc data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:route: data-hd-keyref="route"}
{:row-headers: .row-headers}
{:ruby: .ph data-hd-programlang='ruby'}
{:ruby: data-hd-programlang="ruby"}
{:runtime: architecture="runtime"}
{:runtimeIcon: .runtimeIcon}
{:runtimeIconList: .runtimeIconList}
{:runtimeLink: .runtimeLink}
{:runtimeTitle: .runtimeTitle}
{:screen: .screen}
{:script: data-hd-video='script'}
{:service: architecture="service"}
{:service_instance_name: data-hd-keyref="service_instance_name"}
{:service_name: data-hd-keyref="service_name"}
{:shortdesc: .shortdesc}
{:space_name: data-hd-keyref="space_name"}
{:step: data-tutorial-type='step'}
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:terraform: .ph data-hd-interface='terraform'}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:tutorial: data-hd-content-type='tutorial'}
{:ui: .ph data-hd-interface='ui'}
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vbnet: .ph data-hd-programlang='vb.net'}
{:video: .video}
  
  

# Load balancers
{: #cs_troubleshoot_lb}

As you use {{site.data.keyword.openshiftlong}}, consider these techniques for general load balancer troubleshooting and debugging.
{: shortdesc}

While you troubleshoot, you can use the [{{site.data.keyword.containerlong_notm}} Diagnostics and Debug Tool](/docs/openshift?topic=openshift-debug-tool) to run tests and gather pertinent information from your cluster.
{: tip}

## Classic clusters: Cannot connect to an app via a network load balancer (NLB) service
{: #cs_loadbalancer_fails}

**Infrastructure provider**: <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic

{: tsSymptoms}
<img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> You publicly exposed your app by creating an NLB service in your classic cluster. When you tried to connect to your app by using the public IP address of the NLB, the connection failed or timed out.

{: tsCauses}
Your NLB service might not be working properly for one of the following reasons:

-   The cluster is a free cluster or a standard cluster with only one worker node.
-   The cluster is not fully deployed yet.
-   The configuration script for your NLB service includes errors.

{: tsResolve}
To troubleshoot your NLB service:

1.  Check that you set up a standard cluster that is fully deployed and has at least two worker nodes to ensure high availability for your NLB service.

  ```
  ibmcloud oc worker ls --cluster <cluster_name_or_ID>
  ```
  {: pre}

    In your CLI output, make sure that the **Status** of your worker nodes displays **Ready** and that the **Machine Type** shows a flavor other than **free**.

2. For version 2.0 NLBs: Ensure that you complete the [NLB 2.0 prerequisites](/docs/openshift?topic=openshift-loadbalancer-v2#ipvs_provision).

3. Check the accuracy of the configuration file for your NLB service.
    * Version 2.0 NLBs:
        ```
        apiVersion: v1
        kind: Service
        metadata:
          name: myservice
          annotations:
            service.kubernetes.io/ibm-load-balancer-cloud-provider-enable-features: "ipvs"
        spec:
          type: LoadBalancer
          selector:
            <selector_key>:<selector_value>
          ports:
           - protocol: TCP
             port: 8080
          externalTrafficPolicy: Local
        ```
        {: screen}

        1. Check that you defined **LoadBalancer** as the type for your service.
        2. Check that you included the `service.kubernetes.io/ibm-load-balancer-cloud-provider-enable-features: "ipvs"` annotation.
        3. In the `spec.selector` section of the LoadBalancer service, ensure that the `<selector_key>` and `<selector_value>` is the same as the key/value pair that you used in the `spec.template.metadata.labels` section of your deployment YAML. If labels do not match, the **Endpoints** section in your LoadBalancer service displays **<none>** and your app is not accessible from the internet.
        4. Check that you used the **port** that your app listens on.
        5. Check that you set `externalTrafficPolicy` to `Local`.

    * Version 1.0 NLBs:
        ```
        apiVersion: v1
        kind: Service
        metadata:
          name: myservice
        spec:
          type: LoadBalancer
          selector:
            <selector_key>:<selector_value>
          ports:
           - protocol: TCP
             port: 8080
        ```
        {: screen}

        1. Check that you defined **LoadBalancer** as the type for your service.
        2. In the `spec.selector` section of the LoadBalancer service, ensure that the `<selector_key>` and `<selector_value>` is the same as the key/value pair that you used in the `spec.template.metadata.labels` section of your deployment YAML. If labels do not match, the **Endpoints** section in your LoadBalancer service displays **<none>** and your app is not accessible from the internet.
        3. Check that you used the **port** that your app listens on.

3.  Check your NLB service and review the **Events** section to find potential errors.

    ```
    oc describe service <myservice>
    ```
    {: pre}

    Look for the following error messages:

    <ul><li><pre class="screen"><code>Clusters with one node must use services of type NodePort</code></pre></br>To use the NLB service, you must have a standard cluster with at least two worker nodes.</li>
    <li><pre class="screen"><code>No cloud provider IPs are available to fulfill the NLB service request. Add a portable subnet to the cluster and try again</code></pre></br>This error message indicates that no portable public IP addresses are left to be allocated to your NLB service. Refer to <a href="/docs/openshift?topic=openshift-subnets#subnets">Adding subnets to clusters</a> to find information about how to request portable public IP addresses for your cluster. After portable public IP addresses are available to the cluster, the NLB service is automatically created.</li>
    <li><pre class="screen"><code>Requested cloud provider IP &lt;cloud-provider-ip&gt; is not available. The following cloud provider IPs are available: &lt;available-cloud-provider-ips&gt;</code></pre></br>You defined a portable public IP address for your load balancer YAML by using the **`loadBalancerIP`** section, but this portable public IP address is not available in your portable public subnet. In the **`loadBalancerIP`** section your configuration script, remove the existing IP address and add one of the available portable public IP addresses. You can also remove the **`loadBalancerIP`** section from your script so that an available portable public IP address can be allocated automatically.</li>
    <li><pre class="screen"><code>No available nodes for NLB services</code></pre>You do not have enough worker nodes to deploy an NLB service. One reason might be that you deployed a standard cluster with more than one worker node, but the provisioning of the worker nodes failed.</li>
    <ol><li>List available worker nodes.</br><pre class="pre"><code>oc get nodes</code></pre></li>
    <li>If at least two available worker nodes are found, list the worker node details.</br><pre class="pre"><code>ibmcloud oc worker get --cluster &lt;cluster_name_or_ID&gt; --worker &lt;worker_ID&gt;</code></pre></li>
    <li>Make sure that the public and private VLAN IDs for the worker nodes that were returned by the <code>oc get nodes</code> and the <code>ibmcloud oc worker get</code> commands match.</li></ol></li></ul>

4.  If you use a custom domain to connect to your NLB service, make sure that your custom domain is mapped to the public IP address of your NLB service.
    1.  Find the public IP address of your NLB service.
        ```
        oc describe service <service_name> | grep "LoadBalancer Ingress"
        ```
        {: pre}

    2.  Check that your custom domain is mapped to the portable public IP address of your NLB service in the Pointer record (PTR).

<br />

## Classic clusters: Cannot deploy a load balancer
{: #cs_subnet_limit_lb}

**Infrastructure provider**: <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic

{: tsSymptoms}
<img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> When you describe the `ibm-cloud-provider-vlan-ip-config` configmap in your classic cluster, you might see an error message similar to the following example output.
```
oc describe cm ibm-cloud-provider-vlan-ip-config -n kube-system
```
{: pre}
```
Warning  CreatingLoadBalancerFailed ... ErrorSubnetLimitReached: There are already the maximum number of subnets permitted in this VLAN.
```
{: screen}

{: tsCauses}
In standard clusters, the first time that you create a cluster in a zone, a public VLAN and a private VLAN in that zone are automatically provisioned for you in your IBM Cloud infrastructure account. In that zone, 1 public portable subnet is requested on the public VLAN that you specify and 1 private portable subnet is requested on the private VLAN that you specify. For {{site.data.keyword.openshiftlong_notm}}, VLANs have a limit of 40 subnets. If the cluster's VLAN in a zone already reached that limit, you might not have a portable public IP address available to create a network load balancer (NLB).

To view how many subnets a VLAN has:
1.  From the [IBM Cloud infrastructure console](https://cloud.ibm.com/classic?), select **Network** > **IP Management** > **VLANs**.
2.  Click the **VLAN Number** of the VLAN that you used to create your cluster. Review the **Subnets** section to see whether 40 or more subnets exist.

{: tsResolve}
If you need a new VLAN, order one by [contacting {{site.data.keyword.cloud_notm}} support](/docs/vlans?topic=vlans-ordering-premium-vlans#ordering-premium-vlans). Then, [create a cluster](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_create) that uses this new VLAN.

If you have another VLAN that is available, you can [set up VLAN spanning](/docs/vlans?topic=vlans-vlan-spanning#vlan-spanning) in your existing cluster. After, you can add new worker nodes to the cluster that use the other VLAN with available subnets. To check if VLAN spanning is already enabled, use the `ibmcloud oc vlan spanning get --region <region>` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_vlan_spanning_get).

If you are not using all the subnets in the VLAN, you can reuse subnets on the VLAN by adding them to your cluster.
1. Check that the subnet that you want to use is available.
  <p class="note">The infrastructure account that you use might be shared across multiple {{site.data.keyword.cloud_notm}} accounts. In this case, even if you run the `ibmcloud oc subnets` command to see subnets with **Bound Clusters**, you can see information only for your clusters. Check with the infrastructure account owner to make sure that the subnets are available and not in use by any other account or team.</p>

2. Use the [`ibmcloud oc cluster subnet add` command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_subnet_add) to make an existing subnet available to your cluster.

3. Verify that the subnet was successfully created and added to your cluster. The subnet CIDR is listed in the **Subnet VLANs** section.
    ```
    ibmcloud oc cluster get --cluster <cluster_name> --show-resources
    ```
    {: pre}

    In this example output, a second subnet was added to the `2234945` public VLAN:
    ```
    Subnet VLANs
    VLAN ID   Subnet CIDR          Public   User-managed
    2234947   10.xxx.xx.xxx/29     false    false
    2234945   169.xx.xxx.xxx/29    true     false
    2234945   169.xx.xxx.xxx/29    true     false
    ```
    {: screen}

4. Verify that the portable IP addresses from the subnet that you added are used for the load balancer's **EXTERNAL-IP**. It might take several minutes for the services to use the portable IP addresses from the newly-added subnet.
  ```
  oc get svc -n kube-system
  ```
  {: pre}

<br />

## Classic clusters: Source IP preservation fails when using tainted nodes
{: #cs_source_ip_fails_lb}

**Infrastructure provider**: <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic

{: tsSymptoms}
<img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> In a classic cluster, you enabled source IP preservation for a [version 1.0 load balancer](/docs/openshift?topic=openshift-loadbalancer#lb_source_ip) service by changing `externalTrafficPolicy` to `Local` in the service's configuration file. However, no traffic reaches the back-end service for your app.

{: tsCauses}
When you enable source IP preservation for load balancer services, the source IP address of the client request is preserved. The service forwards traffic to app pods on the same worker node only to ensure that the request packet's IP address isn't changed. Typically, load balancer service pods are deployed to the same worker nodes that the app pods are deployed to. However, some situations exist where the service pods and app pods might not be scheduled onto the same worker node. If you use [Kubernetes taints](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/){: external} on worker nodes, any pods that don't have a taint toleration are prevented from running on the tainted worker nodes. Source IP preservation might not be working based on the type of taint you used:

* **Edge node taints**: You [added the `dedicated=edge` label](/docs/openshift?topic=openshift-edge#edge_nodes) to two or more worker nodes on each public VLAN in your cluster to ensure that load balancer pods deploy to those worker nodes only. Then, you also [tainted those edge nodes](/docs/openshift?topic=openshift-edge#edge_workloads) to prevent any other workloads from running on edge nodes. However, you didn't add an edge node affinity rule and toleration to your app deployment. Your app pods can't be scheduled on the same tainted nodes as the service pods, and no traffic reaches the back-end service for your app.

* **Custom taints**: You used custom taints on several nodes so that only app pods with that taint toleration can deploy to those nodes. You added affinity rules and tolerations to the deployments of your app and load balancer service so that their pods deploy to only those nodes. However, `ibm-cloud-provider-ip` `keepalived` pods that are automatically created in the `ibm-system` namespace ensure that the load balancer and the app pods are always scheduled onto the same worker node. These `keepalived` pods don't have the tolerations for the custom taints that you used. They can't be scheduled on the same tainted nodes that your app pods are running on, and no traffic reaches the back-end service for your app.

{: tsResolve}
Resolve the issue by choosing one of the following options:

* **Edge node taints**: To ensure that your load balancer and app pods deploy to tainted edge nodes, [add edge node affinity rules and tolerations to your app deployment](/docs/openshift?topic=openshift-loadbalancer#lb_edge_nodes). Load balancer pods have these affinity rules and tolerations by default.

* **Custom taints**: Remove custom taints that the `keepalived` pods don't have tolerations for. Instead, you can [label worker nodes as edge nodes, and then taint those edge nodes](/docs/openshift?topic=openshift-edge).

If you complete one of the above options but the `keepalived` pods are still not scheduled, you can get more information about the `keepalived` pods:

1. Get the `keepalived` pods.
    ```
    oc get pods -n ibm-system
    ```
    {: pre}

2. In the output, look for `ibm-cloud-provider-ip` pods that have a **Status** of `Pending`. Example:
    ```
    ibm-cloud-provider-ip-169-61-XX-XX-55967b5b8c-7zv9t     0/1       Pending   0          2m        <none>          <none>
    ibm-cloud-provider-ip-169-61-XX-XX-55967b5b8c-8ptvg     0/1       Pending   0          2m        <none>          <none>
    ```
    {:screen}

3. Describe each `keepalived` pod and look for the **Events** section. Address any error or warning messages that are listed.
    ```
    oc describe pod ibm-cloud-provider-ip-169-61-XX-XX-55967b5b8c-7zv9t -n ibm-system
    ```
    {: pre}

<br />

## VPC clusters: Cannot connect to an app via load balancer
{: #vpc_ts_lb}

**Infrastructure provider**: <img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC

{: tsSymptoms}
<img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> You publicly exposed your app by creating a Kubernetes `LoadBalancer` service in your VPC cluster. When you try to connect to your app by using the hostname that is assigned to the Kubernetes `LoadBalancer`, the connection fails or times out.

When you run `oc describe svc <kubernetes_lb_service_name>`, you might see a warning message similar to one of the following in the **Events** section:
```
The VPC load balancer that routes requests to this Kubernetes `LoadBalancer` service is offline.
```
{: screen}
```
The VPC load balancer that routes requests to this Kubernetes `LoadBalancer` service was deleted from your VPC.
```
{: screen}

{: tsCauses}
When you create a Kubernetes `LoadBalancer` service in your cluster, a VPC load balancer is automatically created in your VPC. The VPC load balancer routes requests only to the app that the Kubernetes `LoadBalancer` service exposes. Requests cannot be routed to your app in the following situations:
* A VPC security group is blocking incoming traffic to your worker nodes, including incoming requests to your app.
* The VPC load balancer is offline, such as due to load balancer provisioning errors or VSI connection errors.
* The VPC load balancer is deleted through the VPC console or the CLI.
* The VPC load balancer's DNS entry is still registering.
* You reached the maximum number of VPC load balancers permitted per account. Across all of your VPC clusters in your VPC, a maximum of 20 VPC load balancers can be created.

{: tsResolve}
Verify that no VPC security groups are blocking traffic to your cluster and that the VPC load balancer is available.

1. <img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC clusters that run {{site.data.keyword.openshiftshort}} version 4.4 or earlier: [Allow traffic requests that are routed by the VPC load balancer to node ports on your worker nodes](/docs/openshift?topic=openshift-vpc-network-policy#security_groups).

2. Verify that the VPC load balancer for the Kubernetes `LoadBalancer` service exists. In the output, look for the VPC load balancer that is formatted `kube-<cluster_ID>-<kubernetes_lb_service_UID>`. You can get the Kubernetes `LoadBalancer` service UID by running `oc get svc <service_name> -o yaml`.
  ```
  ibmcloud is load-balancers
  ```
  {: pre}
  * If the VPC load balancer is not listed, it does not exist for one of the following reasons:
      * You reached the maximum number of VPC load balancers permitted per account. Across all of your VPC clusters in your VPC, a maximum of 20 VPC load balancers can be created. One VPC load balancer is created for each Kubernetes `LoadBalancer` service that you create, and it routes requests to that Kubernetes `LoadBalancer` service only.
      * The VPC load balancer was deleted through the VPC console or the CLI. To re-create the VPC load balancer for your Kubernetes `LoadBalancer` service, restart the Kubernetes master by running `ibmcloud oc cluster master refresh --cluster <cluster_name_or_id>`.
    <p class="tip">If you want to remove the load balancing setup for an app in your VPC cluster, delete the Kubernetes `LoadBalancer` service by running `oc delete svc <kubernetes_lb_service_name>`. The VPC load balancer that is associated with the Kubernetes `LoadBalancer` service is automatically deleted from your VPC.</p>
  * If the VPC load balancer is listed, it might not be responsive for the following reasons:
      * Its DNS entry might still be registering. When a VPC load balancer is created, the hostname is registered through a public DNS. In some cases, it can take several minutes for this DNS entry to be replicated to the specific DNS that your client is using. You can either wait for the hostname to be registered in your DNS, or access the VPC load balancer directly by using one of its IP addresses. To find the VPC load balancer IP addresses, run `ibmcloud is lb <LB_ID>` and look for the **Public IPs** field.
      * If after several minutes you cannot reach the load balancer, it might be offline due to provisioning or connection issues. [Open an {{site.data.keyword.cloud_notm}} support case](https://cloud.ibm.com/unifiedsupport/cases/add). For the type, select **Technical**. For the category, select **Network** in the VPC section. In the description, include your cluster ID and the VPC load balancer ID.

<br />

## VPC clusters: Kubernetes `LoadBalancer` service fails because no IPs are available
{: #vpc_no_lb}

**Infrastructure provider**: <img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC

{: tsSymptoms}
<img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> You publicly exposed your app by creating a Kubernetes `LoadBalancer` service in your VPC cluster. When you run `oc describe svc <kubernetes_lb_service_name>`, you see a warning message in the **Events** section similar to one of the following:
```
The subnet with ID(s) '<subnet_id>' has insufficient available ipv4 addresses.
```
{: screen}

{: tsCauses}
When you create a Kubernetes `LoadBalancer` service in your cluster, a VPC load balancer is automatically created in your VPC. The VPC load balancer puts a floating IP address for your Kubernetes `LoadBalancer` service behind a hostname that you can access your app through.

In VPC clusters, both worker nodes and services are assigned IP addresses from the same subnets. Traffic routing is enabled between subnets, so when all IP addresses in a subnet for a zone are used by worker nodes or services, you can still create new worker nodes or services in that zone because they use IP addresses from subnets in other zones. However, if all IP addresses on all subnets are in use, a new Kubernetes `LoadBalancer` service cannot be successfully provisioned.

{: tsResolve}
After you create a VPC subnet, you cannot resize it or change its IP range. Instead, you must create a larger VPC subnet in one or more zones where you have worker nodes. Then you create a new worker pool using the larger subnets.

1. [Create a new VPC subnet](https://cloud.ibm.com/vpc/provision/network){: external} in the same VPC and in one or more zones where your cluster has worker nodes. Make sure that you create a subnet that can support both the number of worker nodes and services that you plan to create in your cluster. The default CIDR size of each VPC subnet is `/24`, which can support up to 253 worker nodes and services. To check your cluster's VPC and zones, run `ibmcloud oc cluster get --cluster <cluster_name_or_ID>`.

2. Create a new worker pool in your cluster.
   ```
   ibmcloud oc worker-pool create vpc-gen2 --name <name> --cluster <cluster_name_or_ID> --flavor <flavor> --size-per-zone <number_of_worker_nodes> --label <key>=<value>
   ```
   {: pre}

3. Using the ID for the larger subnets that you created in step 1, add the zones to the worker pool. Repeat the following command for each zone and subnet.
    ```
    ibmcloud oc zone add vpc-gen2 --zone <zone> --subnet-id <subnet_id> --cluster <cluster_name_or_ID> --worker-pool <worker_pool_name>
    ```
    {: pre}

4. After a few minutes, verify that your `LoadBalancer` service is successfully provisioned onto one of the new subnets. If the service is provisioned successfully, no `Warning` or `Error` events are displayed.
  ```
  oc describe svc <kubernetes_lb_service_name>
  ```
  {: pre}

<br />

## Classic clusters: OpenVPN server error due to ingress IP address for NLB
{: #rhoks_ts_openvpn_subnet}

**Infrastructure provider**: <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic

{: tsSymptoms}
<img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> You see the following error message.
```
CAE003: Unable to determine the ingress IP address for the network load balancer.
```
{: screen}

{: tsCauses}
The OpenVPN server could not be configured because the router IP address that is created for the network load balancer (NLB) could not be found. The router might not have been assigned an IP address because your cluster does not have a subnet with available portable IP addresses, or the NLB setup did not complete.

{: tsResolve}

**Verify that your cluster has available subnets.**
1.  Check that your cluster has a **Subnet CIDR** for public and private subnets. If you set up a private VLAN-only cluster, you might have only a private subnet.
    ```
    ibmcloud oc cluster get --cluster <cluster_name_or_ID> --show-resources
    ```
    {: pre}

    Example output:
    ```
    Name:                           <cluster_name>   
    ...

    Subnet VLANs
    VLAN ID   Subnet CIDR        Public   User-managed   
    2345678   10.xxx.xx.xxx/29   false    false   
    2876543   169.xx.xxx.xxx/29  true     false
    ```
    {: screen}
2.  If the cluster does not have a subnet, [create a subnet for the cluster](/docs/openshift?topic=openshift-subnets#request) or [add an existing subnet from your account to the cluster](/docs/openshift?topic=openshift-subnets#add-existing).
3.  If the cluster does have a subnet, [check for available portable IP addresses](/docs/openshift?topic=openshift-subnets#review_ip) and if necessary, [add more portable IP address by adding a subnet](/docs/openshift?topic=openshift-subnets#adding_ips).
4.  Refresh the master to restart the OpenVPN setup so that it uses the available subnet.
    ```
    ibmcloud oc cluster master refresh --cluster <cluster_name_or_ID>
    ```
    {: pre}

**Verify that the NLB setup completed successfully.**
1.  Check that the `ibm-cloud-provider-ip-*` pods for the NLB are in a **Running** status.
    ```
    oc get pods -n ibm-system | grep ibm-cloud-provider-ip
    ```
    {: pre}
2.  If a pod is not running, review the **Events** in the pod details to troubleshoot the issue further.
    ```
    oc describe pod -n kube-system <pod_name>
    ```
    {: pre}
3.  After you resolve the NLB pod issue, refresh the master to restart the NLB setup.
    ```
    ibmcloud oc cluster master refresh --cluster <cluster_name_or_ID>
    ```
    {: pre}

<br />

## OpenVPN server error due to NLB DNS
{: #rhoks_ts_openvpn_dns}

**Infrastructure provider**:
  * <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
  * <img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC

{: tsSymptoms}
Could not create a domain name service for the network load balancer (`ibmcloud oc nlb-dns create`) with the following error message:<ul>
<li><code>This action requires the Editor role for the cluster in IBM Cloud Container Service. Contact the IBM Cloud account administrator and request the required Identity and Access user role. (A0008)</code></li>
<li><code>The specified cluster could not be found. (A0006)</code></li>
<li><code>The input parameters in the request body are either incomplete or in the wrong format. Be sure to include all required parameters in your request in JSON format. (E0011)</code></li></ul>

{: tsCauses}
The OpenVPN server could not be configured because a domain name service (DNS) was not created for the network load balancer (NLB).

{: tsResolve}
1.  Check that you have the correct permissions in {{site.data.keyword.cloud_notm}} IAM. If not, contact your account administrator to [assign you the appropriate IAM platform or service access role](/docs/openshift?topic=openshift-users#platform).
    ```
    ibmcloud iam user-policies <my_user_name@example.com>
    ```
    {: pre}
2.  For cluster not found or incorrect input parameter errors, continue to the next step.
3.  Refresh the master so that NLB DNS creation operation is retried.
    ```
    ibmcloud oc cluster master refresh --cluster <cluster_name_or_ID>
    ```
    {: pre}
