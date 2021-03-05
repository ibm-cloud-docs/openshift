---

copyright:
  years: 2014, 2021
lastupdated: "2021-03-05"

keywords: openshift, roks, rhos, rhoks

subcollection: openshift

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



# VPC: Exposing apps with load balancers for VPC
{: #vpc-lbaas}

Set up a Load Balancer for VPC to expose your app on the public or private network.
{: shortdesc}

<img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC load balancers can be created for VPC clusters only, and cannot be created for classic clusters. To load balance in classic clusters, see [Classic: About network load balancers (NLBs)](/docs/openshift?topic=openshift-loadbalancer-about).

## About VPC load balancing in {{site.data.keyword.openshiftlong_notm}}
{: #lbaas_about}

To expose an app in a VPC cluster, you can create a layer 7 Application Load Balancer for VPC. In VPC Gen 2 clusters that run {{site.data.keyword.openshiftshort}} version 4.6 or later, you can optionally create a layer 4 Network Load Balancer for VPC.
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
|Types of load balancers|Public and private|Public|
{: caption="Load balancing options for VPC clusters"}

`*` To preserve the source IP address for an Application Load Balancer for VPC, the `service.kubernetes.io/ibm-load-balancer-cloud-provider-enable-features: "proxy-protocol"` annotation must be specified when the VPC application load balancer is initially created. This annotation is supported for VPC Gen 2 clusters that run {{site.data.keyword.openshiftshort}} version 4.5 or later only.

### Network Load Balancer for VPC
{: #nlb_vpc}

In VPC Gen 2 clusters that run {{site.data.keyword.openshiftshort}} version 4.6 or later, set up a layer-4 [Network Load Balancer for VPC](/docs/vpc?topic=vpc-network-load-balancers) in each zone of your cluster to serve as the external entry point for incoming requests to an app.
{: shortdesc}

VPC network load balancers provide several advantages, such as providing higher throughput and better performance by utilizing direct server return (DSR). With DSR, the worker node can send app response packets directly to the client IP address and skip the network load balancer, decreasing the amount of traffic that the network load balancer must handle. Additionally, the network load balancer supports source IP address preservation on all client requests by default.

When you create a Kubernetes `LoadBalancer` service for an app in your cluster and include the `service.kubernetes.io/ibm-load-balancer-cloud-provider-enable-features: "nlb"` annotation, a VPC network load balancer is created in your VPC outside of your cluster. The VPC network load balancer routes requests for your app through the private NodePorts that are automatically opened on your worker nodes.
* If you create a **public** Kubernetes `LoadBalancer` service, you can access your app from the internet through the hostname that is assigned by the VPC network load balancer to the Kubernetes `LoadBalancer` service in the format `1234abcd-<region>.lb.appdomain.cloud`. Even though your worker nodes are connected to only a private VPC subnet, the VPC network load balancer can receive and route public requests to the service that exposes your app. Note that no public gateway is required on your VPC subnet to allow public requests to your VPC network load balancer. However, if your app must access a public URL, you must attach public gateways to the VPC subnets that your worker nodes are connected to.
* **Private** VPC network load balancers are not supported.

The following diagram illustrates how a user accesses an app from the internet through the VPC network load balancer.

<img src="images/vpc_tutorial_lesson4_lb.png" alt="VPC load balancing for a cluster"/>

1. A request to your app uses the hostname that is assigned to the Kubernetes `LoadBalancer` service by the VPC network load balancer, such as `1234abcd-<region>.lb.appdomain.cloud`.
2. The request is automatically forwarded by the VPC network load balancer to one of the node ports on the worker node, and then to the private IP address of the app pod.
3. If app instances are deployed to multiple worker nodes in the cluster, the network load balancer routes the requests between the app pods on various worker nodes within the same zone.

### Application Load Balancer for VPC
{: #lb_vpc}

Set up a layer-7, multizone [Application Load Balancer for VPC](/docs/vpc?topic=vpc-load-balancers) to serve as the external entry point for incoming requests to an app in your cluster.
{: shortdesc}

Do not confuse the Application Load Balancer for VPC with Ingress applications load balancers (ALBs). VPC application load balancers run outside your cluster in your VPC and are configured by Kubernetes `LoadBalancer` services that you create. [Ingress ALBs](/docs/openshift?topic=openshift-ingress-about) are Ingress controllers that run on worker nodes in your cluster.
{: note}

By default, when you create a Kubernetes `LoadBalancer` service for an app in your cluster, an Application Load Balancer for VPC is created in your VPC outside of your cluster. The VPC application load balancer routes requests to your app through the private NodePorts that are automatically opened on your worker nodes.
* If you create a **public** Kubernetes `LoadBalancer` service, you can access your app from the internet through the hostname that is assigned by the VPC application load balancer to the Kubernetes `LoadBalancer` service in the format `1234abcd-<region>.lb.appdomain.cloud`. Even though your worker nodes are connected to only a private VPC subnet, the VPC application load balancer can receive and route public requests to the service that exposes your app. Note that no public gateway is required on your VPC subnet to allow public requests to your VPC application load balancer. However, if your app must access a public URL, you must attach public gateways to the VPC subnets that your worker nodes are connected to.
* If you create a **private** Kubernetes `LoadBalancer` service, your app is accessible only to systems that are connected to your private subnets within the same region and VPC. If you are connected to your private VPC network, you can access your app through the hostname that is assigned by the VPC application load balancer to the Kubernetes `LoadBalancer` service in the format `1234abcd-<region>.lb.appdomain.cloud`.

The following diagram illustrates how a user accesses an app from the internet through the VPC application load balancer.

<img src="images/vpc_alb.png" alt="VPC load balancing for a cluster"/>

1. A request to your app uses the hostname that is assigned to the Kubernetes `LoadBalancer` service by the VPC application load balancer, such as `1234abcd-<region>.lb.appdomain.cloud`.
2. The request is automatically forwarded by the VPC application load balancer to one of the node ports on the worker node, and then to the private IP address of the app pod.
3. If app instances are deployed to multiple worker nodes in the cluster, the load balancer routes the requests between the app pods on various worker nodes. Additionally, if you have a multizone cluster, the VPC application load balancer routes requests to worker nodes across all subnets and zones in your cluster.

<br />

## Setting up an Application Load Balancer for VPC
{: #setup_vpc_ks_vpc_lb}

Expose your app to the public or to the private network by setting up a Kubernetes `LoadBalancer` service in your cluster. When you expose your app, a Load Balancer for VPC that routes requests to your app is automatically created for you in your VPC outside of your cluster.
{: shortdesc}

Do not confuse the Application Load Balancer for VPC with Ingress applications load balancers (ALBs). VPC application load balancers run outside your cluster in your VPC and are configured by Kubernetes `LoadBalancer` services that you create. [Ingress ALBs](/docs/openshift?topic=openshift-ingress-about) are Ingress controllers that run on worker nodes in your cluster.
{: note}

**Before you begin**:
* Ensure that you have the [**Writer** or **Manager** {{site.data.keyword.cloud_notm}} IAM service access role](/docs/openshift?topic=openshift-users#platform) for the `default` namespace.
* [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).
* <img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC Gen 2 clusters that run {{site.data.keyword.openshiftshort}} version 4.4 or earlier only: [Allow traffic requests that are routed by the VPC application load balancer to node ports on your worker nodes](/docs/openshift?topic=openshift-vpc-network-policy#security_groups).
* To view VPC application load balancers, install the `infrastructure-service` plug-in. The prefix for running commands is `ibmcloud is`.
  ```
  ibmcloud plugin install infrastructure-service
  ```
  {: pre}

</br>**To enable your app to receive public or private requests:**
1.  [Deploy your app to the cluster](/docs/openshift?topic=openshift-openshift_apps). Ensure that you add a label in the metadata section of your deployment configuration file. This custom label identifies all pods where your app runs to include them in the load balancing.

2. Create a configuration YAML file for your Kubernetes `LoadBalancer` service and name the file `myloadbalancer.yaml`.
  ```yaml
  apiVersion: v1
  kind: Service
  metadata:
    name: myloadbalancer
    annotations:
      service.kubernetes.io/ibm-load-balancer-cloud-provider-enable-features: "proxy-protocol"
      service.kubernetes.io/ibm-load-balancer-cloud-provider-ip-type: <public_or_private>
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
    <td>`service.kubernetes.io/ibm-load-balancer-cloud-provider-enable-features: "proxy-protocol"`</td>
    <td>VPC Gen 2 and {{site.data.keyword.openshiftshort}} version 4.5 or later: Annotation to enable the PROXY protocol. The load balancer passes client connection information, including the client IP address, the proxy server IP address, and both port numbers, in request headers to your back-end app. Note that your back-end app must be configured to accept the PROXY protocol. For example, you can configure an NGINX app to accept the PROXY protocol by following [these steps ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.nginx.com/nginx/admin-guide/load-balancer/using-proxy-protocol/).</td>
  </tr>
  <tr>
    <td>`service.kubernetes.io/ibm-load-balancer-cloud-provider-ip-type`</td>
    <td>Annotation to specify a service that accepts public or private requests. If you do not include this annotation, a public `LoadBalancer` is created.</td>
  </tr>
  <tr>
    <td>`service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-node-selector`</td>
    <td>{{site.data.keyword.openshiftshort}} version 4.5 or later: Annotation to specify a worker node label selector. To identify the worker nodes that receive traffic, you can select one of the supported label selector keys. Note that you can include only one label selector in the annotation, and that the selector must be specified in the `"key=value"` format. If this annotation is not specified, all worker nodes in your cluster are configured to receive traffic from the VPC application load balancer. If specified, this annotation takes precedence over the `service.kubernetes.io/ibm-load-balancer-cloud-provider-zone` annotation, and any `dedicated: edge` labels on worker nodes are ignored.<br><br>The following keys are permitted:
      <ul><li>`ibm-cloud.kubernetes.io/internal-ip`</li>
      <li>`ibm-cloud.kubernetes.io/machine-type`</li>
      <li>`ibm-cloud.kubernetes.io/os`</li>
      <li>`ibm-cloud.kubernetes.io/region`</li>
      <li>`ibm-cloud.kubernetes.io/subnet-id`</li>
      <li>`ibm-cloud.kubernetes.io/worker-pool-id`</li>
      <li>`ibm-cloud.kubernetes.io/worker-pool-name`</li>
      <li>`ibm-cloud.kubernetes.io/zone`</li>
      <li>4.6 or later only: `kubernetes.io/arch`</li>
      <li>4.6 or later only: `kubernetes.io/hostname`</li>
      <li>4.6 or later only: `kubernetes.io/os`</li>
      <li>`node.kubernetes.io/instance-type`</li>
      <li>`topology.kubernetes.io/region`</li>
      <li>`topology.kubernetes.io/zone`</li></ul>
    </td>
  </tr>
  <tr>
    <td>`service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-subnet`</td>
    <td>{{site.data.keyword.openshiftshort}} version 4.5 or later: Annotation to specify one or more subnets that the VPC application load balancer service deploys to. If specified, this annotation takes precedence over the `service.kubernetes.io/ibm-load-balancer-cloud-provider-zone` annotation. Note that you can specify a different subnet in the same VPC than the subnets that your cluster is attached to. In this case, even though the VPC application load balancer deploys to a different subnet in the same VPC, the VPC application load balancer can still route traffic to your worker nodes on the cluster subnets. To see subnets in all resource groups, run `ibmcloud oc subnets --provider vpc-gen2 --vpc-id <vpc> --zone <zone>`.</td>
  </tr>
  <tr>
    <td>`service.kubernetes.io/ibm-load-balancer-cloud-provider-zone`</td>
    <td>Annotation to specify a VPC zone that your cluster is attached to. When you specify a zone in this annotation, two processes occur:<ul>
    <li>The VPC application load balancer is deployed to the same subnet in that zone that your worker nodes are connected to.</li>
    <li>Only worker nodes in your cluster in this zone are configured to receive traffic from the VPC application load balancer.</li></ul>
    To see zones, run `ibmcloud oc zone ls --provider vpc-gen2`.<p class="note">To place the load balancer in a specific zone, you must specify this annotation when you create the load balancer. If you later change this annotation to a different zone, the load balancer itself is not moved to the new zone. However, the load balancer is reconfigured to send traffic to only worker nodes in the new zone.</br></br>If the `dedicated: edge` label is set on worker nodes and you specify this annotation, then only edge nodes in the specified zone are configured to receive traffic. Edge nodes in other zones and non-edge nodes in the specified zone do not receive traffic from the load balancer.</p></td>
  </tr>
  <tr>
    <td>`selector`</td>
    <td>The label key (&lt;selector_key&gt;) and value (&lt;selector_value&gt;) that you used in the `spec.template.metadata.labels` section of your app deployment YAML. This custom label identifies all pods where your app runs to include them in the load balancing.</td>
  </tr>
  <tr>
    <td>`port`</td>
    <td>The port that the service listens on.</td>
  </tr>
  <tr>
    <td>`targetPort`</td>
    <td>The port to which the service directs traffic.</td>
  </tr>
  </tbody></table>

3. Create the Kubernetes `LoadBalancer` service in your cluster.
  ```
  oc apply -f myloadbalancer.yaml -n <namespace>
  ```
  {: pre}

4. Verify that the Kubernetes `LoadBalancer` service is created successfully in your cluster. When the service is created, the **LoadBalancer Ingress** field is populated with a hostname that is assigned by the VPC application load balancer.

  **The VPC application load balancer takes a few minutes to provision in your VPC.** You cannot access your app by using the hostname of your Kubernetes `LoadBalancer` service until the VPC application load balancer is fully provisioned.
  {: note}
  ```
  oc describe svc myloadbalancer -n <namespace>
  ```
  {: pre}

  Example CLI output for a public `LoadBalancer` service:
  ```
  Name:                     myvpcalb
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

5. Verify that the VPC application load balancer is created successfully in your VPC. In the output, verify that the VPC application load balancer has an **Operating Status** of `online` and a **Provision Status** of `active`.

  The VPC application load balancer name has a format `kube-<cluster_ID>-<kubernetes_lb_service_UID>`. To see your cluster ID, run `ibmcloud oc cluster get --cluster <cluster_name>`. To see the Kubernetes `LoadBalancer` service UID, run `oc get svc myloadbalancer -o yaml` and look for the **metadata.uid** field in the output. The dashes (-) are removed from the Kubernetes `LoadBalancer` service UID in the VPC application load balancer name.
  {: tip}
  Do not rename any VPC application load balancers that are created automatically for `LoadBalancer` services. If you rename a VPC application load balancer, {{site.data.keyword.containerlong_notm}} automatically creates another VPC application load balancer for the `LoadBalancer` service.
  {: important}
  ```
  ibmcloud is load-balancers
  ```
  {: pre}

  In the following example CLI output, the VPC application load balancer that is named `kube-bsaucubd07dhl66e4tgg-1f4f408ce6d2485499bcbdec0fa2d306` is created for the Kubernetes `LoadBalancer` service:
  ```
  ID                                          Name                                                         Family        Subnets               Is public   Provision status   Operating status   Resource group
  r006-d044af9b-92bf-4047-8f77-a7b86efcb923   kube-bsaucubd07dhl66e4tgg-1f4f408ce6d2485499bcbdec0fa2d306   Application   mysubnet-us-south-3   true        active             online             default
  ```
  {: screen}

6. If you created a public `LoadBalancer` service, curl the hostname of the Kubernetes `LoadBalancer` service that is assigned by the VPC application load balancer that you found in step 4.
  Example:
  ```
  curl 06496f64-us-south.lb.appdomain.cloud:8080
  ```
  {: pre}

  Example output:
  ```
  Hello world from hello-world-deployment-5fd7787c79-sl9hn! Your app is up and running in a cluster!
  ```
  {: screen}

  If you created a private `LoadBalancer` service, you must be [connected to your private VPC network](/docs/vpc?topic=vpc-vpn-onprem-example) to curl the hostname.
  {: tip}

Do not delete the subnets that you attached to your cluster during cluster creation or when you add worker nodes in a zone. If you delete a VPC subnet that your cluster used, any load balancers that use IP addresses from the subnet might experience issues, and you might be unable to create new load balancers.
{: important}

<br />

## Registering a VPC load balancer with a DNS subdomain and TLS certificate
{: #vpc_lb_dns}

The VPC load balancer provides a default HTTP hostname in the format `1234abcd-<region>.lb.appdomain.cloud` through which you can access your app. However, if you want a TLS certificate for your app domain to support HTTPS, you can create an IBM-provided subdomain or bring your own custom domain for both public and private VPC load balancers.
{: shortdesc}

After you create a DNS subdomain for a VPC load balancer hostname, you cannot use `nlb-dns health-monitor` commands to create a custom health check. Instead, the default VPC load balancer health check that is provided for the default VPC load balancer hostname is used. For more information, see the [VPC documentation](/docs/vpc?topic=vpc-alb-health-checks).
{: note}

Before you begin:
* [Set up a VPC application load balancer](#setup_vpc_ks_vpc_lb). Ensure that you define an HTTPS port in your Kubernetes `LoadBalancer` service that configures the VPC load balancer.
* To use the TLS certificate to access your app via HTTPS, your app must be able to terminate TLS connections.

To register a VPC load balancer hostname with a DNS subdomain:

1. Get the hostname for your VPC load balancer. In the output, look for the hostname in the **EXTERNAL-IP** column.
  ```
  oc get svc -o wide
  ```
  {: pre}

  Example output:
  ```
  NAME            TYPE           CLUSTER-IP       EXTERNAL-IP                            PORT(S)     AGE       SELECTOR
  ...
  webserver-lb    LoadBalancer   172.21.xxx.xxx   1234abcd-us-south.lb.appdomain.cloud   8080:30532/TCP     1d       run=webserver
  ```
  {: screen}

2. Create a DNS subdomain for the load balancer hostname.
  * **IBM-provided subdomain**: Use `nlb-dns` commands to generate a subdomain with a TLS certificate for the VPC load balancer hostname. {{site.data.keyword.cloud_notm}} takes care of generating and maintaining the wildcard TLS certificate for the subdomain for you.
    1. Create a DNS subdomain and TLS certificate.
      ```
      ibmcloud oc nlb-dns create vpc-gen2 --cluster <cluster_name_or_id> --lb-host <vpc_lb_hostname> --type (public|private)
      ```
      {: pre}

    2. Verify that the subdomain is created. For more information, see [Understanding the subdomain format](/docs/openshift?topic=openshift-loadbalancer_hostname#loadbalancer_hostname_format).
      ```
      ibmcloud oc nlb-dns ls --cluster <cluster_name_or_id>
      ```
      {: pre}

      Example output:
      ```
      Subdomain                                                                               Load Balancer Hostname                        Health Monitor   SSL Cert Status           SSL Cert Secret Name
      mycluster-a1b2cdef345678g9hi012j3kl4567890-0001.us-south.containers.appdomain.cloud     ["1234abcd-us-south.lb.appdomain.cloud"]      None             created                   <certificate>
      ```
      {: screen}

  * **Custom domain**: Provide your own custom domain and give it an alias by specifying the load balancer hostname as a Canonical Name record (CNAME).
    1. Register a custom domain by working with your Domain Name Service (DNS) provider or [{{site.data.keyword.cloud_notm}} DNS](/docs/dns?topic=dns-getting-started).
    2. Define an alias for your custom domain by specifying the load balancer hostname as a Canonical Name record (CNAME).

3. If you created a subdomain for a public VPC load balancer, open a web browser and enter the URL to access your app through the subdomain. If you created a subdomain for a private VPC application load balancer, you must be [connected to your private VPC network](/docs/vpc?topic=vpc-vpn-onprem-example) to test access to your subdomain.

To use the TLS certificate to access your app via HTTPS, ensure that you defined an HTTPS port in your [Kubernetes `LoadBalancer` service](#setup_vpc_ks_vpc_lb). You can verify that requests are correctly routing through the HTTPS port by running `curl -v --insecure https://<domain>`. A connection error indicates that no HTTPS port is open on the service. Also, ensure that TLS connections can be terminated by your app. You can verify that your app terminates TLS properly by running `curl -v https://<domain>`. A certificate error indicates that your app is not properly terminating TLS connections.
{: tip}

<br />

## Limitations
{: #lbaas_limitations}

Review the following default settings and limitations.
{: shortdesc}

* All VPC load balancers do not currently support UDP.
* **Kubernetes 1.20 and later**: Although the Kubernetes [SCTP protocol](https://kubernetes.io/docs/concepts/services-networking/service/#sctp){: external} and [application protocol](https://kubernetes.io/docs/concepts/services-networking/service/#application-protocol){: external} features are generally available in the community release, creating load balancers that use these protocols is not supported in {{site.data.keyword.containerlong_notm}} clusters.
* Private VPC application load balancers do not accept all traffic, only RFC 1918 traffic.
* One VPC load balancer is created for each Kubernetes `LoadBalancer` service that you create, and it routes requests to that Kubernetes `LoadBalancer` service only. Across all of your VPC clusters in your VPC, a maximum of 20 VPC load balancers can be created.
* The VPC load balancer can route requests to pods that are deployed on a maximum of 50 worker nodes in a cluster.
  * If your cluster has more than 50 worker nodes and you set `externalTrafficPolicy: Cluster` when you configured the Kubernetes `LoadBalancer` service, the VPC load balancer can only route to the first 50 worker nodes that are returned in the cluster's API call to the VPC load balancer.
  * If your cluster has more than 50 worker nodes and you set `externalTrafficPolicy: Local` when you configured the Kubernetes `LoadBalancer` service, the VPC load balancer fails and cannot forward traffic to any worker nodes. Instead, create one load balancer per zone. In each Kubernetes `LoadBalancer` service that you create, include the `service.kubernetes.io/ibm-load-balancer-cloud-provider-zone: "<zone>"` annotation. Each load balancer can forward requests to apps on the worker nodes in that zone only, and can forwards requests to a maximum of 50 worker nodes in that zone.
* When you define the configuration YAML file for a Kubernetes `LoadBalancer` service, the following annotations and settings are not supported:
    * `service.kubernetes.io/ibm-load-balancer-cloud-provider-vlan: "<vlan_id>"`
    * `service.kubernetes.io/ibm-load-balancer-cloud-provider-enable-features: "ipvs"`
    * `service.kubernetes.io/ibm-load-balancer-cloud-provider-ipvs-scheduler: "<algorithm>"`
    * `spec.loadBalancerIP`
    * `spec.loadBalancerSourceRanges`
    * The `externalTrafficPolicy: Local` setting is supported, but the setting does not preserve the source IP of the request.
* When you delete a VPC cluster, any VPC load balancers that were automatically created by {{site.data.keyword.openshiftlong_notm}} for the Kubernetes `LoadBalancer` services in that cluster are also automatically deleted. However, any VPC load balancers that you manually created in your VPC are not deleted.
* You can register up to 128 subdomains for VPC load balancer hostnames. This limit can be lifted on request by opening a [support case](/docs/get-support?topic=get-support-using-avatar).



