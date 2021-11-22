---

copyright: 
  years: 2014, 2021
lastupdated: "2021-11-22"

keywords: openshift

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# VPC: Exposing apps with load balancers for VPC
{: #vpc-lbaas}

Set up a Load Balancer for VPC to expose your app on the public or private network.
{: shortdesc}

![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC load balancers can be created for VPC clusters only, and can't be created for classic clusters. To load balance in classic clusters, see [Classic: About network load balancers (NLBs)](/docs/containers?topic=containers-loadbalancer-about).

## About VPC load balancing in {{site.data.keyword.openshiftlong_notm}}
{: #lbaas_about}

To expose an app in a VPC cluster, you can create a layer 7 Application Load Balancer for VPC. In VPC clusters that run {{site.data.keyword.openshiftshort}} version 4.6 or later, you can optionally create a layer 4 Network Load Balancer for VPC.
{: shortdesc}

The following table describes the basic characteristics of each load balancing option.

|Characteristic|Application Load Balancer for VPC|Network Load Balancer for VPC|
|--------------|---------------------|-----------------------------|
|Supported {{site.data.keyword.openshiftshort}} version|All versions|4.6 and later only|
|Transport layer|Layer 7|Layer 4|
|Supported protocols|TCP|TCP|
|Application access|Hostname|Hostname and static IP address|
|Source IP preservation|Configurable*|Yes|
|Improved performance with direct server return|No|Yes|
|Multizone routing|Yes|No|
|Types of load balancers|Public and private|Public and private|
{: caption="Load balancing options for VPC clusters"}

`*` To preserve the source IP address for an Application Load Balancer for VPC, the `service.kubernetes.io/ibm-load-balancer-cloud-provider-enable-features: "proxy-protocol"` annotation must be specified when the VPC ALB is initially created. This annotation is supported for VPC clusters that run {{site.data.keyword.openshiftshort}} version 4.5 or later only.

### Network Load Balancer for VPC
{: #nlb_vpc}

In VPC clusters that run {{site.data.keyword.openshiftshort}} version 4.6 or later, set up a layer-4 [Network Load Balancer for VPC](/docs/vpc?topic=vpc-network-load-balancers) (VPC NLB) in each zone of your cluster to serve as the external entry point for incoming requests to an app.
{: shortdesc}

VPC NLBs provide several advantages, such as providing higher throughput and better performance by utilizing direct server return (DSR). With DSR, the worker node can send app response packets directly to the client IP address and skip the VPC NLB, decreasing the amount of traffic that the VPC NLB must handle. Additionally, the VPC NLB supports source IP address preservation on all client requests by default.

When you create a Kubernetes `LoadBalancer` service for an app in your cluster and include the `service.kubernetes.io/ibm-load-balancer-cloud-provider-enable-features: "nlb"` annotation, a VPC NLB is created in your VPC outside of your cluster. The VPC NLB routes requests for your app through the private NodePorts that are automatically opened on your worker nodes.
* If you create a **public** Kubernetes `LoadBalancer` service, you can access your app from the internet through the external, public IP address that is assigned by the VPC NLB to the Kubernetes `LoadBalancer` service. Even though your worker nodes are connected to only a private VPC subnet, the VPC NLB can receive and route public requests to the service that exposes your app. Note that no public gateway is required on your VPC subnet to allow public requests to your VPC NLB. However, if your app must access a public URL, you must attach public gateways to the VPC subnets that your worker nodes are connected to.
* If you create a **private** Kubernetes `LoadBalancer` service, your app is accessible only to systems that are connected to your private subnets within the same region and VPC. If you are connected to your private VPC network, you can access your app through the external, private IP address that is assigned by the VPC NLB to the Kubernetes `LoadBalancer` service.

The following diagram illustrates how a user accesses an app from the internet through the VPC NLB.

<img src="images/vpc_tutorial_lesson4_lb.png" alt="VPC load balancing for a cluster through the VPC NLB"/>

1. A request to your app uses the external IP address that is assigned to the Kubernetes `LoadBalancer` service by the VPC NLB.
2. The request is automatically forwarded by the VPC NLB to one of the node ports on the worker node, and then to the private IP address of the app pod.
3. If app instances are deployed to multiple worker nodes in the cluster, the VPC NLB routes the requests between the app pods on various worker nodes within the same zone.

### Application Load Balancer for VPC
{: #lb_vpc}

Set up a layer-7, multizone [Application Load Balancer for VPC](/docs/vpc?topic=vpc-load-balancers) (VPC ALB) to serve as the external entry point for incoming requests to an app in your cluster.
{: shortdesc}

Do not confuse the Application Load Balancer for VPC with {{site.data.keyword.openshiftlong_notm}} Ingress applications load balancers. Application Load Balancers for VPC (VPC ALBs) run outside your cluster in your VPC and are configured by Kubernetes `LoadBalancer` services that you create. [Ingress applications load balancers (ALBs)](/docs/containers?topic=containers-ingress-about) are Ingress controllers that run on worker nodes in your cluster.
{: note}

By default, when you create a Kubernetes `LoadBalancer` service for an app in your cluster, an Application Load Balancer for VPC is created in your VPC outside of your cluster. The VPC ALB routes requests to your app through the private NodePorts that are automatically opened on your worker nodes.
* If you create a **public** Kubernetes `LoadBalancer` service, you can access your app from the internet through the hostname that is assigned by the VPC ALB to the Kubernetes `LoadBalancer` service in the format `1234abcd-<region>.lb.appdomain.cloud`. Even though your worker nodes are connected to only a private VPC subnet, the VPC ALB can receive and route public requests to the service that exposes your app. Note that no public gateway is required on your VPC subnet to allow public requests to your VPC ALB. However, if your app must access a public URL, you must attach public gateways to the VPC subnets that your worker nodes are connected to.
* If you create a **private** Kubernetes `LoadBalancer` service, your app is accessible only to systems that are connected to your private subnets within the same region and VPC. If you are connected to your private VPC network, you can access your app through the hostname that is assigned by the VPC ALB to the Kubernetes `LoadBalancer` service in the format `1234abcd-<region>.lb.appdomain.cloud`.

The following diagram illustrates how a user accesses an app from the internet through the VPC ALB.

<img src="images/vpc_alb.png" alt="VPC load balancing for a cluster through the VPC ALB"/>

1. A request to your app uses the hostname that is assigned to the Kubernetes `LoadBalancer` service by the VPC ALB, such as `1234abcd-<region>.lb.appdomain.cloud`.
2. The request is automatically forwarded by the VPC ALB to one of the node ports on the worker node, and then to the private IP address of the app pod.
3. If app instances are deployed to multiple worker nodes in the cluster, the load balancer routes the requests between the app pods on various worker nodes. Additionally, if you have a multizone cluster, the VPC ALB routes requests to worker nodes across all subnets and zones in your cluster.



## Setting up a Network Load Balancer for VPC
{: #setup_vpc_nlb}

Expose your app to the public or to the private network by setting up a [public](#setup_vpc_nlb_pub) or [private](#setup_vpc_nlb_priv) Kubernetes `LoadBalancer` service in each zone of your VPC cluster. Then, you can optionally [register the VPC NLB with a DNS record and TLS certificate](#vpc_nlb_dns).
{: shortdesc}

### Setting up a public VPC NLB
{: #setup_vpc_nlb_pub}

Expose your app to public network traffic by setting up a Kubernetes `LoadBalancer` service in each zone of your cluster. When you create the Kubernetes `LoadBalancer` service, a public Network Load Balancer for VPC (VPC NLB) that routes requests to your app is automatically created for you in your VPC outside of your cluster.
{: shortdesc}

**Before you begin**:
* VPC NLBs can be created only in VPC clusters that run {{site.data.keyword.openshiftshort}} version 4.6 or later.
* Ensure that you have the [**Writer** or **Manager** {{site.data.keyword.cloud_notm}} IAM service access role](/docs/openshift?topic=openshift-users#checking-perms) for the namespace in which you deploy the Kubernetes `LoadBalancer` service for the VPC NLB.
* [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).
* To view VPC NLBs, install the `infrastructure-service` plug-in. The prefix for running commands is `ibmcloud is`.
    ```sh
    ibmcloud plugin install infrastructure-service
    ```
    {: pre}

</br>**To enable your app to receive public requests:**

1. [Deploy your app to the cluster](/docs/containers?topic=containers-deploy_app#app_cli). Ensure that you add a label in the metadata section of your deployment configuration file. This custom label identifies all pods where your app runs to include them in the load balancing.

2. Create a configuration YAML file for your Kubernetes `LoadBalancer` service. Consider naming the service in the format `<app_name>-vpc-nlb-<VPC_zone>`.
    ```yaml
    apiVersion: v1
    kind: Service
    metadata:
      name: <app_name>-vpc-nlb-<VPC_zone>
      annotations:
        service.kubernetes.io/ibm-load-balancer-cloud-provider-enable-features: "nlb"
        service.kubernetes.io/ibm-load-balancer-cloud-provider-ip-type: "public"
        service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-node-selector: "<key>=<value>"
        service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-subnets: "<subnet1_ID,subnet2_ID>"
        service.kubernetes.io/ibm-load-balancer-cloud-provider-zone: "<zone>"
    spec:
      type: LoadBalancer
      selector:
        <selector_key>: <selector_value>
      ports:
       - name: http
         protocol: TCP
         port: 8080
         targetPort: 8080
       - name: https
         protocol: TCP
         port: 443
      externalTrafficPolicy: Local
    ```
    {: codeblock}

    <table summary="The columns are read from left to right. The first column has the parameter of the YAML file. The second column describes the parameter.">
    <caption>Understanding the YAML file components</caption>
    <col width="25%">
    <thead>
    <th>Parameter</th>
    <th>Description</th>
    </thead>
    <tbody>
    <tr>
        <td><code>service.kubernetes.io/ibm-load-balancer-cloud-provider-enable-features: "nlb"</code></td>
    <td>Required: Annotation to create a VPC NLB.</td>
    </tr>
    <tr>
        <td><code>service.kubernetes.io/ibm-load-balancer-cloud-provider-ip-type</code></td>
    <td>Optional: Annotation to specify a service that accepts public requests. If you don't include this annotation, a public VPC NLB is created.</td>
    </tr>
    <tr>
        <td><code>service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-node-selector</code></td>
    <td>Optional: Annotation to specify a worker node label selector. To identify the worker nodes that receive traffic, you can select one of the supported label selector keys. Note that you can include only one label selector in the annotation, and that the selector must be specified in the <code>"key=value"</code> format. If this annotation is not specified, all worker nodes in the same zone as the VPC NLB are configured to receive traffic from the VPC NLB. If specified, this annotation takes precedence over the <code>service.kubernetes.io/ibm-load-balancer-cloud-provider-zone</code> annotation, and any <code>dedicated: edge</code> labels on worker nodes are ignored.<br><br>The following keys are permitted:
        <ul><li><code>ibm-cloud.kubernetes.io/internal-ip</code></li>
        <li><code>ibm-cloud.kubernetes.io/machine-type</code></li>
        <li><code>ibm-cloud.kubernetes.io/os</code></li>
        <li><code>ibm-cloud.kubernetes.io/region</code></li>
        <li><code>ibm-cloud.kubernetes.io/subnet-id</code></li>
        <li><code>ibm-cloud.kubernetes.io/worker-pool-id</code></li>
        <li><code>ibm-cloud.kubernetes.io/worker-pool-name</code></li>
        <li><code>ibm-cloud.kubernetes.io/zone</code></li>
        <li><code>kubernetes.io/arch</code></li>
        <li><code>kubernetes.io/hostname</code></li>
        <li><code>kubernetes.io/os</code></li>
        <li><code>node.kubernetes.io/instance-type</code></li>
        <li><code>topology.kubernetes.io/region</code></li>
        <li><code>topology.kubernetes.io/zone</code></li></ul>
        </td>
    </tr>
    <tr>
        <td><code>service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-subnets</code></td>
    <td>Optional: Annotation to specify one or more subnets in one zone that the VPC NLB deploys to. Values can be specified as VPC subnet IDs, VPC subnet names, or VPC subnet CIDRs. If specified, this annotation takes precedence over the <code>service.kubernetes.io/ibm-load-balancer-cloud-provider-zone</code> annotation. Note that you can specify a different subnet in the same VPC than the subnets that your cluster is attached to. In this case, even though the VPC NLB deploys to a different subnet in the same VPC, the VPC NLB can still route traffic to your worker nodes on the cluster subnets in the same zone. To see subnets in all resource groups, run <code>ibmcloud oc subnets --provider vpc-gen2 --vpc-id &lt;vpc&gt; --zone &lt;zone&gt;</code>.</td>
    </tr>
    <tr>
        <td><code>service.kubernetes.io/ibm-load-balancer-cloud-provider-zone</code></td>
    <td>Optional: Annotation to specify a VPC zone that your cluster is attached to. The VPC NLB is deployed to the same subnet in that zone that your worker nodes are connected to. Because the VPC NLB is single-zone, only worker nodes in your cluster in this zone are configured to receive traffic.
    <p>To see zones, run <code>ibmcloud oc zone ls --provider vpc-gen2</code>.If you later change this annotation to a different zone, the VPC NLB is not moved to the new zone.</br></br>Note that if you don't specify this annotation or the <code>service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-subnets</code> annotation, the VPC NLB is deployed to the most optimal zone. For example, the VPC NLB is deployed only to zones in which worker nodes exist and are in the <code>Ready</code> state.</p></td>
    </tr>
    <tr>
        <td><code>selector</code></td>
    <td>The label key (&lt;selector_key&gt;) and value (&lt;selector_value&gt;) that you used in the <code>spec.template.metadata.labels</code> section of your app deployment YAML. This custom label identifies all pods where your app runs to include them in the load balancing.</td>
    </tr>
    <tr>
        <td><code>port</code></td>
    <td>The port that the service listens on.</td>
    </tr>
    <tr>
        <td><code>targetPort</code></td>
    <td>Optional: The port to which the service directs traffic.</td>
    </tr>
    <tr>
        <td><code>externalTrafficPolicy: Local</code></td>
    <td><ul><li>Set to <code>Local</code> to preserve the source IP address of client requests to your apps. You must ensure that an app pod exists on each worker node in the zone that the VPC NLB deploys to, such as by using a DaemonSet.</li><li>If <code>Cluster</code> is set, DSR is implemented only from the worker node that the VPC NLB initially forwards the incoming request to. Once the incoming request arrives, the request is forwarded to a worker node that contains the app pod. The response from the app pod is sent to the original worker node, and that worker node uses DSR to send the response directly back to the client, bypassing the VPC NLB.</li></ul></td>
    </tr>
    </tbody></table>

3. Create the Kubernetes `LoadBalancer` service in your cluster.
    ```sh
    oc apply -f <filename>.yaml -n <namespace>
    ```
    {: pre}

4. Verify that the Kubernetes `LoadBalancer` service is created successfully in your cluster. When the service is created, the **LoadBalancer Ingress** field is populated with an external IP address that is assigned by the VPC NLB.

    **The VPC NLB takes a few minutes to provision in your VPC.** The external IP address of your Kubernetes `LoadBalancer` service might be `pending` until the VPC NLB is fully provisioned.
    {: note}

    ```sh
    oc describe svc myloadbalancer -n <namespace>
    ```
    {: pre}

    Example CLI output for a public `LoadBalancer` service:
    ```sh
    NAME:                     myvpcnlb
    Namespace:                default
    Labels:                   <none>
    Annotations:              service.kubernetes.io/ibm-load-balancer-cloud-provider-enable-features: nlb
    Selector:                 app=echo-server
    Type:                     LoadBalancer
    IP:                       172.21.204.12
    LoadBalancer Ingress:     169.XXX.XXX.XXX
    Port:                     tcp-80  80/TCP
    TargetPort:               8080/TCP
    NodePort:                 tcp-80  32022/TCP
    Endpoints:                172.17.17.133:8080,172.17.22.68:8080,172.17.34.18:8080 + 3 more...
    Session Affinity:         None
    External Traffic Policy:  Local
    HealthCheck NodePort:     30882
    Events:
        Type     Reason                           Age                  From                Message
    ----     ------                           ----                 ----                -------
    Warning  SyncLoadBalancerFailed           13m (x5 over 15m)    service-controller  Error syncing load balancer: failed to ensure load balancer: kube-bqcssbbd0bsui62odcdg-2d93b07decf641d2ad3f9c2985122ec1 for service default/myvpcnlb is busy: offline/create_pending
    Normal   EnsuringLoadBalancer             9m27s (x7 over 15m)  service-controller  Ensuring load balancer
    Normal   EnsuredLoadBalancer              9m20s                service-controller  Ensured load balancer
    Normal   CloudVPCLoadBalancerNormalEvent  8m17s                ibm-cloud-provider  Event on cloud load balancer myvpcnlb for service default/myvpcnlb with UID 2d93b07d-ecf6-41d2-ad3f-9c2985122ec1: The VPC load balancer that routes requests to this Kubernetes LoadBalancer service is currently online/active.
    ```
    {: screen}

5. Verify that the VPC NLB is created successfully in your VPC. In the output, verify that the VPC NLB has an **Operating Status** of `online` and a **Provision Status** of `active`.

    The VPC NLB name has a format `kube-<cluster_ID>-<kubernetes_lb_service_UID>`. To see your cluster ID, run `ibmcloud oc cluster get --cluster <cluster_name>`. To see the Kubernetes `LoadBalancer` service UID, run `oc get svc myloadbalancer -o yaml` and look for the **metadata.uid** field in the output. The dashes (-) are removed from the Kubernetes `LoadBalancer` service UID in the VPC NLB name.
    {: tip}

    Do not rename any VPC NLBs that are created automatically for `LoadBalancer` services. If you rename a VPC NLB, {{site.data.keyword.openshiftshort}} automatically creates another VPC NLB for the `LoadBalancer` service.
    {: important}

    ```sh
    ibmcloud is load-balancers
    ```
    {: pre}

    In the following example CLI output, the VPC NLB that is named `kube-bh077ne10vqpekt0domg-046e0f754d624dca8b287a033d55f96e` is created for the Kubernetes `LoadBalancer` service:
    ```
    ID                                     Name                                                         Created          Host Name                                  Is Public   Listeners                               Operating Status   Pools                                   Private IPs              Provision Status   Public IPs                    Subnets                                Resource Group
    06496f64-a689-4693-ba23-320959b7b677   kube-bh077ne10vqpekt0domg-046e0f754d624dca8b287a033d55f96e   8 minutes ago    1234abcd-us-south.lb.appdomain.cloud       yes         95482dcf-6b9b-4c6a-be54-04d3c46cf017    online             717f2122-5431-403c-b21d-630a12fc3a5a    10.241.0.7               active             169.63.99.184                 c6540331-1c1c-40f4-9c35-aa42a98fe0d9   00809211b934565df546a95f86160f62
    ```
    {: screen}

6. Access the IP address of the Kubernetes `LoadBalancer` service that you found in step 4 and your app port in the format `<external_IP>:<app_port>`.

7. Optional: Repeat these steps to deploy a public VPC NLB in each zone where you want to expose your app. Then, you can register the external IP addresses of the VPC NLB in each zone with one [DNS subdomain](#vpc_nlb_dns).

Do not delete the subnets that you attached to your cluster during cluster creation or when you add worker nodes in a zone. If you delete a VPC subnet that your cluster used, any VPC NLBs that use IP addresses from the subnet might experience issues, and you might be unable to create new load balancers.
{: important}

### Setting up a private VPC NLB
{: #setup_vpc_nlb_priv}

Expose your app to private network traffic by setting up a Kubernetes `LoadBalancer` service in each zone of your cluster. When you create the Kubernetes `LoadBalancer` service, a private Network Load Balancer for VPC (VPC NLB) that routes requests to your app is automatically created for you in your VPC outside of your cluster.
{: shortdesc}

**Before you begin**:
* VPC NLBs can be created only in VPC clusters that run {{site.data.keyword.openshiftshort}} version 4.6 or later.
* Ensure that you have the [**Writer** or **Manager** {{site.data.keyword.cloud_notm}} IAM service access role](/docs/openshift?topic=openshift-users#checking-perms) for the namespace in which you deploy the Kubernetes `LoadBalancer` service for the VPC NLB.
* Connect to your VPC private network, such as through a [VPC VPN connection](/docs/containers?topic=containers-vpc-vpnaas).
* [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).
* To view VPC NLBs, install the `infrastructure-service` plug-in. The prefix for running commands is `ibmcloud is`.
    ```sh
    ibmcloud plugin install infrastructure-service
    ```
    {: pre}

</br>

**To enable your app to receive private network requests:**

1. Create a VPC subnet that is dedicated to your VPC NLB. This subnet must exist in the same VPC and location as your cluster, but can't be attached to your cluster or any worker nodes.
    1. From the [VPC subnet dashboard](https://cloud.ibm.com/vpc/network/subnets){: external}, click **New subnet**.
    2. Enter a name for your subnet.
    3. Select the location where your cluster exists and the zone where you want to create the VPC NLB.
    4. Select the name of the VPC where your cluster exists.
    5. Specify the number of IP addresses to create. Because this subnet is dedicated to the VPC NLB, you might choose a smaller size, such as 16. You can't change the number of IPs that a VPC subnet has later. If you enter a specific IP range, don't use the following reserved ranges: `172.16.0.0/16`, `172.18.0.0/16`, `172.19.0.0/16`, and `172.20.0.0/16`.
    6. Click **Create subnet**. After the subnet is provisioned, note its **ID**.

2. If the client that must connect to your app through the VPC NLB exists outside of the VPC and zone that you created the dedicated VPC subnet in, you must create a custom ingress routing table. Private VPC NLBs might add rules to the custom routing table to ensure service availability for some failure conditions. For more information, see the table in the [known limitations](/docs/vpc?topic=vpc-nlb-limitations) and [About routing tables and routes](/docs/vpc?topic=vpc-about-custom-routes).
    1. From the [VPC routing tables dashboard](https://cloud.ibm.com/vpc-ext/network/routingTables){: external}, click **Create**.
    2. Enter a name for your routing table.
    3. Select the location and zone where you created the dedicated subnet.
    4. Select the name of the VPC where your subnet exists.
    5. For the **Traffic type**, select **Ingress**.
    6. Depending from where the client is accessing your app, choose a **Traffic source**. For more information about setting up connections to your VPC private network, see the [documentation](/docs/containers?topic=containers-vpc-vpnaas) for choosing the {{site.data.keyword.vpc_short}} VPN, {{site.data.keyword.tg_short}}, or {{site.data.keyword.dl_short}} for VPC connectivity.
        * On-premises network: **Direct link**
        * Another VPC or classic infrastructure: **Transit gateway**
        * Another zone within the same VPC:    **VPC zone**

3. [Deploy your app to the cluster](/docs/containers?topic=containers-deploy_app#app_cli). Ensure that you add a label in the metadata section of your deployment configuration file. This custom label identifies all pods where your app runs to include them in the load balancing.

4. Create a configuration YAML file for your Kubernetes `LoadBalancer` service. Consider naming the service in the format `<app_name>-vpc-nlb-<VPC_zone>`.
    ```yaml
    apiVersion: v1
    kind: Service
    metadata:
      name: <app_name>-vpc-nlb-<VPC_zone>
      annotations:
        service.kubernetes.io/ibm-load-balancer-cloud-provider-enable-features: "nlb"
        service.kubernetes.io/ibm-load-balancer-cloud-provider-ip-type: "private"
        service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-subnets: "<subnet_ID>"
        service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-node-selector: "<key>=<value>"
    spec:
      type: LoadBalancer
      selector:
        <selector_key>: <selector_value>
      ports:
       - name: http
         protocol: TCP
         port: 8080
         targetPort: 8080
       - name: https
         protocol: TCP
         port: 443
      externalTrafficPolicy: Local
    ```
    {: codeblock}

    <table summary="The columns are read from left to right. The first column has the parameter of the YAML file. The second column describes the parameter.">
    <caption>Understanding the YAML file components</caption>
    <col width="25%">
    <thead>
    <th>Parameter</th>
    <th>Description</th>
    </thead>
    <tbody>
    <tr>
        <td><code>service.kubernetes.io/ibm-load-balancer-cloud-provider-enable-features: "nlb"</code></td>
    <td>Required: Annotation to create a VPC NLB.</td>
    </tr>
    <tr>
        <td><code>service.kubernetes.io/ibm-load-balancer-cloud-provider-ip-type: "private"</code></td>
    <td>Required: Annotation to specify a service that accepts private requests.</td>
    </tr>
    <tr>
        <td><code>service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-subnets</code></td>
    <td>Required: Annotation to specify the dedicated subnet that the VPC NLB deploys to. The value can be specified as a VPC subnet ID, VPC subnet name, or VPC subnet CIDR. You must specify only one subnet. The subnet must exist in the same VPC as your cluster and in a zone where your cluster has worker nodes, but no worker nodes can be attached to this subnet. The worker nodes that exist in the same zone as this subnet are configured to receive traffic from the VPC NLB. To see subnets in all resource groups, run <code>ibmcloud oc subnets --provider vpc-gen2 --vpc-id &lt;vpc&gt; --zone &lt;zone&gt;</code>.</td>
    </tr>
    <tr>
        <td><code>service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-node-selector</code></td>
    <td>Optional: Annotation to specify a worker node label selector. Within the same zone as the dedicated subnet for the VPC NLB, you can configure specific worker nodes to receive traffic by selecting one of the supported label selector keys. Note that you can include only one label selector in the annotation, and that the selector must be specified in the <code>"key=value"</code> format. If this annotation is not specified, all worker nodes in the same zone as the VPC subnet that you specified in the <code>service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-subnets</code> annotation are configured to receive traffic from the VPC NLB. If specified, any <code>dedicated: edge</code> labels on worker nodes are ignored.<br><br>The following keys are permitted:
        <ul><li><code>ibm-cloud.kubernetes.io/internal-ip</code></li>
        <li><code>ibm-cloud.kubernetes.io/machine-type</code></li>
        <li><code>ibm-cloud.kubernetes.io/os</code></li>
        <li><code>ibm-cloud.kubernetes.io/region</code></li>
        <li><code>ibm-cloud.kubernetes.io/subnet-id</code></li>
        <li><code>ibm-cloud.kubernetes.io/worker-pool-id</code></li>
        <li><code>ibm-cloud.kubernetes.io/worker-pool-name</code></li>
        <li><code>ibm-cloud.kubernetes.io/zone</code></li>
        <li><code>kubernetes.io/arch</code></li>
        <li><code>kubernetes.io/hostname</code></li>
        <li><code>kubernetes.io/os</code></li>
        <li><code>node.kubernetes.io/instance-type</code></li>
        <li><code>topology.kubernetes.io/region</code></li>
        <li><code>topology.kubernetes.io/zone</code></li></ul>
        </td>
    </tr>
    <tr>
        <td><code>selector</code></td>
    <td>The label key (&lt;selector_key&gt;) and value (&lt;selector_value&gt;) that you used in the <code>spec.template.metadata.labels</code> section of your app deployment YAML. This custom label identifies all pods where your app runs to include them in the load balancing.</td>
    </tr>
    <tr>
        <td><code>port</code></td>
    <td>The port that the service listens on.</td>
    </tr>
    <tr>
        <td><code>targetPort</code></td>
    <td>Optional: The port to which the service directs traffic.</td>
    </tr>
    <tr>
        <td><code>externalTrafficPolicy: Local</code></td>
    <td><ul><li>Set to <code>Local</code> to preserve the source IP address of client requests to your apps. You must ensure that an app pod exists on each worker node in the zone that the VPC NLB deploys to, such as by using a DaemonSet, and the source of requests to your apps must exist outside of the cluster.</li><li>If <code>Cluster</code> is set, DSR is implemented only from the worker node that the VPC NLB initially forwards the incoming request to. Once the incoming request arrives, the request is forwarded to a worker node that contains the app pod. The response from the app pod is sent to the original worker node, and that worker node uses DSR to send the response directly back to the client, bypassing the VPC NLB.</li></ul></td>
    </tr>
    </tbody></table>

5. Create the Kubernetes `LoadBalancer` service in your cluster.
    ```sh
    oc apply -f <filename>.yaml -n <namespace>
    ```
    {: pre}

6. Verify that the Kubernetes `LoadBalancer` service is created successfully in your cluster. When the service is created, the **LoadBalancer Ingress** field is populated with an external IP address that is assigned by the VPC NLB.

    **The VPC NLB takes a few minutes to provision in your VPC.** The external IP address of your Kubernetes `LoadBalancer` service might be `pending` until the VPC NLB is fully provisioned.
    {: note}

    ```sh
    oc describe svc myloadbalancer -n <namespace>
    ```
    {: pre}

    Example CLI output for a private `LoadBalancer` service:
    ```sh
    NAME:                     myvpcnlb
    Namespace:                default
    Labels:                   <none>
    Annotations:              service.kubernetes.io/ibm-load-balancer-cloud-provider-enable-features: nlb
    Selector:                 app=echo-server
    Type:                     LoadBalancer
    IP:                       172.21.204.12
    LoadBalancer Ingress:     10.XXX.XXX.XXX
    Port:                     tcp-80  80/TCP
    TargetPort:               8080/TCP
    NodePort:                 tcp-80  32022/TCP
    Endpoints:                172.17.17.133:8080,172.17.22.68:8080,172.17.34.18:8080 + 3 more...
    Session Affinity:         None
    External Traffic Policy:  Local
    HealthCheck NodePort:     30882
    Events:
        Type     Reason                           Age                  From                Message
    ----     ------                           ----                 ----                -------
    Warning  SyncLoadBalancerFailed           13m (x5 over 15m)    service-controller  Error syncing load balancer: failed to ensure load balancer: kube-bqcssbbd0bsui62odcdg-2d93b07decf641d2ad3f9c2985122ec1 for service default/myvpcnlb is busy: offline/create_pending
    Normal   EnsuringLoadBalancer             9m27s (x7 over 15m)  service-controller  Ensuring load balancer
    Normal   EnsuredLoadBalancer              9m20s                service-controller  Ensured load balancer
    Normal   CloudVPCLoadBalancerNormalEvent  8m17s                ibm-cloud-provider  Event on cloud load balancer myvpcnlb for service default/myvpcnlb with UID 2d93b07d-ecf6-41d2-ad3f-9c2985122ec1: The VPC load balancer that routes requests to this Kubernetes LoadBalancer service is currently online/active.
    ```
    {: screen}

7. Verify that the VPC NLB is created successfully in your VPC. In the output, verify that the VPC NLB has an **Operating Status** of `online` and a **Provision Status** of `active`.

    The VPC NLB name has a format `kube-<cluster_ID>-<kubernetes_lb_service_UID>`. To see your cluster ID, run `ibmcloud oc cluster get --cluster <cluster_name>`. To see the Kubernetes `LoadBalancer` service UID, run `oc get svc myloadbalancer -o yaml` and look for the **metadata.uid** field in the output. The dashes (-) are removed from the Kubernetes `LoadBalancer` service UID in the VPC NLB name.
    {: tip}

    Do not rename any VPC NLBs that are created automatically for `LoadBalancer` services. If you rename a VPC NLB, {{site.data.keyword.openshiftshort}} automatically creates another VPC NLB for the `LoadBalancer` service.
    {: important}

    ```sh
    ibmcloud is load-balancers
    ```
    {: pre}

    In the following example CLI output, the VPC NLB that is named `kube-bh077ne10vqpekt0domg-046e0f754d624dca8b287a033d55f96e` is created for the Kubernetes `LoadBalancer` service:
    ```
    ID                                     Name                                                         Created          Host Name                                  Is Public   Listeners                               Operating Status   Pools                                   Private IPs              Provision Status   Public IPs                    Subnets                                Resource Group
    06496f64-a689-4693-ba23-320959b7b677   kube-bh077ne10vqpekt0domg-046e0f754d624dca8b287a033d55f96e   8 minutes ago    1234abcd-us-south.lb.appdomain.cloud       no         95482dcf-6b9b-4c6a-be54-04d3c46cf017    online             717f2122-5431-403c-b21d-630a12fc3a5a    10.XXX.XXX.XXX           active             -               c6540331-1c1c-40f4-9c35-aa42a98fe0d9   00809211b934565df546a95f86160f62
    ```
    {: screen}

8. From your connection to the VPC private network, access the IP address of the Kubernetes `LoadBalancer` service that you found in step 6 and your app port in the format `<external_IP>:<app_port>`.

9. Optional: Repeat these steps to deploy a private VPC NLB in each zone where you want to expose your app. Then, you can register the external IP addresses of the VPC NLB in each zone with one [DNS subdomain](#vpc_nlb_dns).

### Registering a DNS record and TLS certificate
{: #vpc_nlb_dns}

VPC NLBs provide static external IP addresses through which you can access your app. To register an SSL certificate for your app domain to support HTTPS, you can create an IBM-provided subdomain or bring your own custom domain.
{: shortdesc}

For example, say that you have a multizone cluster, and run replicas of your app on worker nodes in each zone of your cluster. You [create one VPC NLB](#setup_vpc_nlb) per zone to expose the app replicas. Then, you can register the external IP addresses provided by each VPC NLB with one DNS entry.

After you create a DNS subdomain for VPC NLBs, you can't use `nlb-dns health-monitor` commands to create a custom health check. Instead, the default VPC health check is used. For more information, see the [VPC documentation](/docs/vpc?topic=vpc-nlb-health-checks).
{: note}

**Before you begin:**
* [Create one VPC NLB](#setup_vpc_nlb) per zone for your app. Ensure that you define an HTTPS port in your Kubernetes `LoadBalancer` service that configures the VPC NLB.
* To use the SSL certificate to access your app via HTTPS, your app must be able to terminate TLS connections.

**To register VPC NLB IP addresses with a DNS subdomain**:

1. Retrieve the external IP address of your load balancer.

```sh
oc get svc -o wide
```
{: pre}

Example output
```
NAME                      TYPE           CLUSTER-IP       EXTERNAL-IP       PORT(S)            AGE      SELECTOR
...
myapp-vpc-nlb-jp-tok-3    LoadBalancer   172.21.xxx.xxx   169.xx.xxx.xx     8080:30532/TCP     1d       run=webserver
```
{: screen}

2. Create a custom or IBM-provided DNS subdomain for the IP address.

    - **Custom domain**:
        1. Register a custom domain by working with your Domain Name Service (DNS) provider or [{{site.data.keyword.cloud_notm}} DNS](/docs/dns?topic=dns-getting-started).
        2. Define an alias for your custom domain by specifying the load balancer IP addresses as A records.

    - **IBM-provided subdomain**: Use `nlb-dns` commands to generate a subdomain with an SSL certificate for the IP addresses. {{site.data.keyword.cloud_notm}} takes care of generating and maintaining the wildcard SSL certificate for the subdomain for you.

        1. Create a DNS subdomain and SSL certificate.
            ```sh
            ibmcloud oc nlb-dns create vpc-gen2 --type public --cluster <cluster_name_or_id> --ip <vpc_nlb1_ip> --ip <vpc_nlb2_ip> --ip <vpc_nlb3_ip>
            ```
            {: pre}
        2. Verify that the subdomain is created. For more information, see [Understanding the subdomain format](/docs/openshift?topic=openshift-loadbalancer_hostname#loadbalancer_hostname_format).
            ```sh
            ibmcloud oc nlb-dns ls --cluster <cluster_name_or_id>
            ```
            {: pre}

            Example output
            ```sh
            Subdomain                                                                               IP(s)                                        Health Monitor   SSL Cert Status           SSL Cert Secret Name
            mycluster-a1b2cdef345678g9hi012j3kl4567890-0001.us-south.containers.appdomain.cloud     169.46.xx.x,169.48.xxx.xx,169.48.xxx.xx      None             created                   <certificate>
            ```
            {: screen}

3. Open a web browser and enter the URL to access your app through the subdomain.

To use the SSL certificate to access your app via HTTPS, ensure that you defined an HTTPS port in your [Kubernetes `LoadBalancer` service](#setup_vpc_ks_vpc_lb). You can verify that requests are correctly routing through the HTTPS port by running `curl -v --insecure https://<domain>`. A connection error indicates that no HTTPS port is open on the service. Also, ensure that TLS connections can be terminated by your app. You can verify that your app terminates TLS properly by running `curl -v https://<domain>`. A certificate error indicates that your app is not properly terminating TLS connections.
{: tip}



## Setting up an Application Load Balancer for VPC
{: #setup_vpc_ks_vpc_lb}

Expose your app to the public or to the private network by setting up a Kubernetes `LoadBalancer` service in your cluster. When you expose your app, an Application Load Balancer for VPC (VPC ALB) that routes requests to your app is automatically created for you in your VPC outside of your cluster.
{: shortdesc}

Do not confuse the Application Load Balancer for VPC with {{site.data.keyword.openshiftlong_notm}} Ingress applications load balancers. Application Load Balancers for VPC (VPC ALBs) run outside your cluster in your VPC and are configured by Kubernetes `LoadBalancer` services that you create. [Ingress applications load balancers (ALBs)](/docs/containers?topic=containers-ingress-about) are Ingress controllers that run on worker nodes in your cluster.
{: note}

### Setting up a public or private VPC ALB
{: #setup_vpc_alb_pub_priv}

**Before you begin**:
* Ensure that you have the [**Writer** or **Manager** {{site.data.keyword.cloud_notm}} IAM service access role](/docs/openshift?topic=openshift-users#checking-perms) for the namespace in which you deploy the Kubernetes `LoadBalancer` service for the VPC NLB.
* [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).
* ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC clusters that run {{site.data.keyword.openshiftshort}} version 4.4 or earlier only: [Allow traffic requests that are routed by the VPC ALB to node ports on your worker nodes](/docs/openshift?topic=openshift-vpc-network-policy#security_groups).
* To view VPC ALBs, install the `infrastructure-service` plug-in. The prefix for running commands is `ibmcloud is`.
    ```sh
    ibmcloud plugin install infrastructure-service
    ```
    {: pre}

</br>**To enable your app to receive public or private requests:**
1. [Deploy your app to the cluster](/docs/openshift?topic=openshift-openshift_apps). Ensure that you add a label in the metadata section of your deployment configuration file. This custom label identifies all pods where your app runs to include them in the load balancing.

2. Create a configuration YAML file for your Kubernetes `LoadBalancer` service and name the file `myloadbalancer.yaml`.
    ```yaml
    apiVersion: v1
    kind: Service
    metadata:
      name: myloadbalancer
      annotations:
        service.kubernetes.io/ibm-load-balancer-cloud-provider-enable-features: "proxy-protocol"
        service.kubernetes.io/ibm-load-balancer-cloud-provider-ip-type: "<public_or_private>"
        service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-node-selector: "<key>=<value>"
        service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-subnets: "<subnet1_ID,subnet2_ID>"
        service.kubernetes.io/ibm-load-balancer-cloud-provider-zone: "<zone>"
   spec:
     type: LoadBalancer
     selector:
        <selector_key>: <selector_value>
     ports:
       - name: http
         protocol: TCP
         port: 8080
         targetPort: 8080
       - name: https
         protocol: TCP
         port: 443
    ```
    {: codeblock}

    <table summary="The columns are read from left to right. The first column has the parameter of the YAML file. The second column describes the parameter.">
    <caption>Understanding the YAML file components</caption>
    <col width="25%">
    <thead>
    <th>Parameter</th>
    <th>Description</th>
    </thead>
    <tbody>
    <tr>
        <td><code>service.kubernetes.io/ibm-load-balancer-cloud-provider-enable-features: "proxy-protocol"</code></td>
    <td>VPC and {{site.data.keyword.openshiftshort}} version 4.5 or later: Annotation to enable the PROXY protocol. The load balancer passes client connection information, including the client IP address, the proxy server IP address, and both port numbers, in request headers to your back-end app. Note that your back-end app must be configured to accept the PROXY protocol. For example, you can configure an NGINX app to accept the PROXY protocol by following <a href="https://docs.nginx.com/nginx/admin-guide/load-balancer/using-proxy-protocol/">these steps</a> <img src="../icons/launch-glyph.svg" alt="External link icon">.</td>
    </tr>
    <tr>
        <td><code>service.kubernetes.io/ibm-load-balancer-cloud-provider-ip-type</code></td>
    <td>Annotation to specify a service that accepts public or private requests. If you don't include this annotation, a public <code>LoadBalancer</code> is created.</td>
    </tr>
    <tr>
        <td><code>service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-node-selector</code></td>
    <td>{{site.data.keyword.openshiftshort}} version 4.5 or later: Annotation to specify a worker node label selector. To identify the worker nodes that receive traffic, you can select one of the supported label selector keys. Note that you can include only one label selector in the annotation, and that the selector must be specified in the <code>"key=value"</code> format. If this annotation is not specified, all worker nodes in your cluster are configured to receive traffic from the VPC ALB. If specified, this annotation takes precedence over the <code>service.kubernetes.io/ibm-load-balancer-cloud-provider-zone</code> annotation, and any <code>dedicated: edge</code> labels on worker nodes are ignored.<br><br>The following keys are permitted:
        <ul><li><code>ibm-cloud.kubernetes.io/internal-ip</code></li>
        <li><code>ibm-cloud.kubernetes.io/machine-type</code></li>
        <li><code>ibm-cloud.kubernetes.io/os</code></li>
        <li><code>ibm-cloud.kubernetes.io/region</code></li>
        <li><code>ibm-cloud.kubernetes.io/subnet-id</code></li>
        <li><code>ibm-cloud.kubernetes.io/worker-pool-id</code></li>
        <li><code>ibm-cloud.kubernetes.io/worker-pool-name</code></li>
        <li><code>ibm-cloud.kubernetes.io/zone</code></li>
        <li>4.6 or later only: <code>kubernetes.io/arch</code></li>
        <li>4.6 or later only: <code>kubernetes.io/hostname</code></li>
        <li>4.6 or later only: <code>kubernetes.io/os</code></li>
        <li><code>node.kubernetes.io/instance-type</code></li>
        <li><code>topology.kubernetes.io/region</code></li>
        <li><code>topology.kubernetes.io/zone</code></li></ul>
        </td>
    </tr>
    <tr>
        <td><code>service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-subnets</code></td>
    <td>{{site.data.keyword.openshiftshort}} version 4.5 or later: Annotation to specify one or more subnets that the VPC ALB service deploys to. If specified, this annotation takes precedence over the <code>service.kubernetes.io/ibm-load-balancer-cloud-provider-zone</code> annotation. Note that you can specify a different subnet in the same VPC than the subnets that your cluster is attached to. In this case, even though the VPC ALB deploys to a different subnet in the same VPC, the VPC ALB can still route traffic to your worker nodes on the cluster subnets. To see subnets in all resource groups, run <code>ibmcloud oc subnets --provider vpc-gen2 --vpc-id &lt;vpc&gt; --zone &lt;zone&gt;</code>.</td>
    </tr>
    <tr>
        <td><code>service.kubernetes.io/ibm-load-balancer-cloud-provider-zone</code></td>
    <td>Annotation to specify a VPC zone that your cluster is attached to. When you specify a zone in this annotation, two processes occur:<ul>
        <li>The VPC ALB is deployed to the same subnet in that zone that your worker nodes are connected to.</li>
        <li>Only worker nodes in your cluster in this zone are configured to receive traffic from the VPC ALB.</li></ul>
        <p>To see zones, run <code>ibmcloud oc zone ls --provider vpc-gen2</code>.</p>    
        <p>To place the load balancer in a specific zone, you must specify this annotation when you create the load balancer. If you later change this annotation to a different zone, the load balancer itself is not moved to the new zone. However, the load balancer is reconfigured to send traffic to only worker nodes in the new zone.</p>
        <p>If the <code>dedicated: edge</code> label is set on worker nodes and you specify this annotation, then only edge nodes in the specified zone are configured to receive traffic. Edge nodes in other zones and non-edge nodes in the specified zone don't receive traffic from the load balancer.</p>
    </td>
    </tr>
    <tr>
        <td><code>selector</code></td>
    <td>The label key (&lt;selector_key&gt;) and value (&lt;selector_value&gt;) that you used in the <code>spec.template.metadata.labels</code> section of your app deployment YAML. This custom label identifies all pods where your app runs to include them in the load balancing.</td>
    </tr>
    <tr>
        <td><code>port</code></td>
    <td>The port that the service listens on.</td>
    </tr>
    <tr>
        <td><code>targetPort</code></td>
    <td>The port to which the service directs traffic.</td>
    </tr>
    </tbody></table>
    


3. Create the Kubernetes `LoadBalancer` service in your cluster.
    ```sh
    oc apply -f myloadbalancer.yaml -n <namespace>
    ```
    {: pre}

4. Verify that the Kubernetes `LoadBalancer` service is created successfully in your cluster. When the service is created, the **LoadBalancer Ingress** field is populated with a hostname that is assigned by the VPC ALB.

    **The VPC ALB takes a few minutes to provision in your VPC.** You can't access your app by using the hostname of your Kubernetes `LoadBalancer` service until the VPC ALB is fully provisioned.
    {: note}

    ```sh
    oc describe svc myloadbalancer -n <namespace>
    ```
    {: pre}

    Example CLI output for a public `LoadBalancer` service:
    ```sh
    NAME:                     myvpcalb
    Namespace:                default
    Labels:                   <none>
    Annotations:              
    Selector:                 app=echo-server
    Type:                     LoadBalancer
    IP:                       172.21.XX.XX
    LoadBalancer Ingress:     1234abcd-us-south.lb.appdomain.cloud
    Port:                     tcp-80  80/TCP
    TargetPort:               8080/TCP
    NodePort:                 tcp-80  30610/TCP
    Endpoints:                172.17.17.133:8080,172.17.22.68:8080,172.17.34.18:8080 + 3 more...
    Session Affinity:         None
    External Traffic Policy:  Local
    HealthCheck NodePort:     31438
    Events:
        Type    Reason                           Age   From                Message
    ----    ------                           ----  ----                -------
    Normal  EnsuringLoadBalancer             16m   service-controller  Ensuring load balancer
    Normal  EnsuredLoadBalancer              15m   service-controller  Ensured load balancer
    Normal  CloudVPCLoadBalancerNormalEvent  13m   ibm-cloud-provider  Event on cloud load balancer myvpcalb for service default/myvpcalb with UID 08cbacf0-2c93-4186-84b6-c4ab88a2faf9: The VPC load balancer that routes requests to this Kubernetes LoadBalancer service is currently online/active.
    ```
    {: screen}

5. Verify that the VPC ALB is created successfully in your VPC. In the output, verify that the VPC ALB has an **Operating Status** of `online` and a **Provision Status** of `active`.

    The VPC ALB name has a format `kube-<cluster_ID>-<kubernetes_lb_service_UID>`. To see your cluster ID, run `ibmcloud oc cluster get --cluster <cluster_name>`. To see the Kubernetes `LoadBalancer` service UID, run `oc get svc myloadbalancer -o yaml` and look for the **metadata.uid** field in the output. The dashes (-) are removed from the Kubernetes `LoadBalancer` service UID in the VPC ALB name.
    {: tip}

    Do not rename any VPC ALBs that are created automatically for `LoadBalancer` services. If you rename a VPC ALB, {{site.data.keyword.openshiftshort}} automatically creates another VPC ALB for the `LoadBalancer` service.
    {: important}

    ```sh
    ibmcloud is load-balancers
    ```
    {: pre}

    In the following example CLI output, the VPC ALB that is named `kube-bsaucubd07dhl66e4tgg-1f4f408ce6d2485499bcbdec0fa2d306` is created for the Kubernetes `LoadBalancer` service:
    ```
    ID                                          Name                                                         Family        Subnets               Is public   Provision status   Operating status   Resource group
    r006-d044af9b-92bf-4047-8f77-a7b86efcb923   kube-bsaucubd07dhl66e4tgg-1f4f408ce6d2485499bcbdec0fa2d306   Application   mysubnet-us-south-3   true        active             online             default
    ```
    {: screen}

6. If you created a public `LoadBalancer` service, curl the hostname of the Kubernetes `LoadBalancer` service that is assigned by the VPC ALB that you found in step 4.
    Example:
    ```sh
    curl 06496f64-us-south.lb.appdomain.cloud:8080
    ```
    {: pre}

    Example output

    ```sh
    Hello world from hello-world-deployment-5fd7787c79-sl9hn! Your app is up and running in a cluster!
    ```
    {: screen}

    If you created a private `LoadBalancer` service, you must be [connected to your private VPC network](/docs/vpc?topic=vpc-vpn-onprem-example) to curl the hostname.
    {: tip}

Do not delete the subnets that you attached to your cluster during cluster creation or when you add worker nodes in a zone. If you delete a VPC subnet that your cluster used, any load balancers that use IP addresses from the subnet might experience issues, and you might be unable to create new load balancers.
{: important}



### Registering a DNS record and TLS certificate
{: #vpc_lb_dns}

The Application Load Balancer for VPC (VPC ALB) provides a default HTTP hostname in the format `1234abcd-<region>.lb.appdomain.cloud` through which you can access your app. However, if you want a TLS certificate for your app domain to support HTTPS, you can create an IBM-provided subdomain or bring your own custom domain for both public and private VPC ALBs.
{: shortdesc}

After you create a DNS subdomain for a VPC ALB hostname, you can't use `nlb-dns health-monitor` commands to create a custom health check. Instead, the default VPC load balancer health check that is provided for the default VPC ALB hostname is used. For more information, see the [VPC documentation](/docs/vpc?topic=vpc-alb-health-checks).
{: note}

**Before you begin**:
* [Set up a VPC ALB](#setup_vpc_ks_vpc_lb). Ensure that you define an HTTPS port in your Kubernetes `LoadBalancer` service that configures the VPC ALB.
* To use the TLS certificate to access your app via HTTPS, your app must be able to terminate TLS connections.

**To register a VPC ALB hostname with a DNS subdomain:**

1. Retrieve the hostname for your VPC ALB by running the `get svc` command. In the output, look for the hostname in the **EXTERNAL-IP** column.
    ```sh
    oc get svc -o wide
    ```
    {: pre}

    Example output

    ```sh
    NAME            TYPE           CLUSTER-IP       EXTERNAL-IP                            PORT(S)     AGE       SELECTOR
    ...
    webserver-lb    LoadBalancer   172.21.xxx.xxx   1234abcd-us-south.lb.appdomain.cloud   8080:30532/TCP     1d       run=webserver
    ```
    {: screen}

2. Create a custom or IBM-provided DNS subdomain for the load balancer hostname.
    - **Custom domain**: Provide your own custom domain and give it an alias by specifying the load balancer hostname as a Canonical Name record (CNAME).
        1. Register a custom domain by working with your Domain Name Service (DNS) provider or [{{site.data.keyword.cloud_notm}} DNS](/docs/dns?topic=dns-getting-started).
        2. Define an alias for your custom domain by specifying the load balancer hostname as a Canonical Name record (CNAME).

    - **IBM-provided subdomain**: Use `nlb-dns` commands to generate a subdomain with a TLS certificate for the VPC ALB hostname. {{site.data.keyword.cloud_notm}} takes care of generating and maintaining the wildcard TLS certificate for the subdomain for you.
        1. Create a DNS subdomain and TLS certificate.
            ```sh
            ibmcloud oc nlb-dns create vpc-gen2 --cluster <cluster_name_or_id> --lb-host <vpc_lb_hostname> --type (public|private)
            ```
            {: pre}
        2. Verify that the subdomain is created. For more information, see [Understanding the subdomain format](/docs/openshift?topic=openshift-loadbalancer_hostname#loadbalancer_hostname_format).
            ```sh
            ibmcloud oc nlb-dns ls --cluster <cluster_name_or_id>
            ```
            {: pre}

            Example output
            ```sh
            Subdomain                                                                               Load Balancer Hostname                        Health Monitor   SSL Cert Status           SSL Cert Secret Name
            mycluster-a1b2cdef345678g9hi012j3kl4567890-0001.us-south.containers.appdomain.cloud     ["1234abcd-us-south.lb.appdomain.cloud"]      None             created                   <certificate>
            ```
            {: screen}

3. If you created a subdomain for a public VPC ALB, open a web browser and enter the URL to access your app through the subdomain. If you created a subdomain for a private VPC ALB, you must be [connected to your private VPC network](/docs/vpc?topic=vpc-vpn-onprem-example) to test access to your subdomain.

To use the TLS certificate to access your app via HTTPS, ensure that you defined an HTTPS port in your [Kubernetes `LoadBalancer` service](#setup_vpc_ks_vpc_lb). You can verify that requests are correctly routing through the HTTPS port by running `curl -v --insecure https://<domain>`. A connection error indicates that no HTTPS port is open on the service. Also, ensure that TLS connections can be terminated by your app. You can verify that your app terminates TLS properly by running `curl -v https://<domain>`. A certificate error indicates that your app is not properly terminating TLS connections.
{: tip}



## Limitations
{: #lbaas_limitations}

Review the following default settings and limitations.
{: shortdesc}

* Review [known limitations for VPC ALBs](/docs/vpc?topic=vpc-lb-limitations) and [known limitations for VPC NLBs](/docs/vpc?topic=vpc-nlb-limitations).
* Private VPC ALBs don't accept all traffic, only RFC 1918 traffic.
* Private VPC NLBs must be created on a dedicated VPC subnet that must exist in the same VPC and location as your cluster, but the subnet can't be attached to your cluster or any worker nodes.
* All VPC load balancers don't currently support UDP.
* {{site.data.keyword.openshiftshort}} 4.6 or later: Although the Kubernetes [SCTP protocol](https://kubernetes.io/docs/concepts/services-networking/service/#sctp){: external} and [application protocol](https://kubernetes.io/docs/concepts/services-networking/service/#application-protocol){: external} features are generally available in the community release, creating load balancers that use these protocols is not supported in {{site.data.keyword.containerlong_notm}} clusters.
* One VPC load balancer is created for each Kubernetes `LoadBalancer` service that you create, and it routes requests to that Kubernetes `LoadBalancer` service only. Across all your VPC clusters in your VPC, a maximum of 50 VPC load balancers can be created. For more information, see the [VPC quotas documentation](/docs/vpc?topic=vpc-quotas#load-balancer-quotas).
* The VPC load balancer can route requests to pods that are deployed on a maximum of 50 worker nodes in a cluster.
    * If your cluster has more than 50 worker nodes and you set `externalTrafficPolicy: Cluster` when you configured the Kubernetes `LoadBalancer` service, the VPC load balancer can only route to the first 50 worker nodes that are returned in the cluster's API call to the VPC load balancer.
    * If your cluster has more than 50 worker nodes and you set `externalTrafficPolicy: Local` when you configured the Kubernetes `LoadBalancer` service, the VPC load balancer fails and can't forward traffic to any worker nodes. Instead, create one load balancer per zone. In each Kubernetes `LoadBalancer` service that you create, include the `service.kubernetes.io/ibm-load-balancer-cloud-provider-zone: "<zone>"` annotation. Each load balancer can forward requests to apps on the worker nodes in that zone only, and can forwards requests to a maximum of 50 worker nodes in that zone.
* When you define the configuration YAML file for a Kubernetes `LoadBalancer` service, the following annotations and settings are not supported:
    * `service.kubernetes.io/ibm-load-balancer-cloud-provider-vlan: "<vlan_id>"`
    * `service.kubernetes.io/ibm-load-balancer-cloud-provider-enable-features: "ipvs"`
    * `service.kubernetes.io/ibm-load-balancer-cloud-provider-ipvs-scheduler: "<algorithm>"`
    * `spec.loadBalancerIP`
    * `spec.loadBalancerSourceRanges`
    * VPC NLBs only: `service.kubernetes.io/ibm-load-balancer-cloud-provider-enable-features: "proxy-protocol"`
    * VPC ALBs only: The `externalTrafficPolicy: Local` setting is supported, but the setting does not preserve the source IP of the request.
* When you delete a VPC cluster, any VPC load balancers that were automatically created by {{site.data.keyword.openshiftlong_notm}} for the Kubernetes `LoadBalancer` services in that cluster are also automatically deleted. However, any VPC load balancers that you manually created in your VPC are not deleted.
* You can register up to 128 subdomains for VPC load balancer hostnames. This limit can be lifted on request by opening a [support case](/docs/get-support?topic=get-support-using-avatar).
* {{site.data.keyword.openshiftshort}} 4.6 or later: Subdomains that you register for VPC load balancers are limited to 130 characters or fewer.




