---

copyright:
  years: 2014, 2021
lastupdated: "2021-10-14"

keywords: openshift, roks, rhoks, rhos, networking

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

  

# Choosing an app exposure service
{: #cs_network_planning}

Securely expose your apps to external traffic by using {{site.data.keyword.openshiftshort}} routes or {{site.data.keyword.containerlong}} NodePort, network load balancer, or Ingress application load balancer services.
{: shortdesc}

## Understanding options for exposing apps
{: #external}

To securely expose your apps to external traffic, you can use choose from the following services.
{: shortdesc}

[{{site.data.keyword.openshiftshort}} route](/docs/openshift?topic=openshift-openshift_routes)
:   A route exposes a service as a hostname in the format `<service_name>-<project>.<cluster_name>-<random_hash>-0001.<region>.containers.appdomain.cloud`. A router is deployed by default to your cluster, which enable routes to be used by external clients. The router uses the service selector to find the service and the endpoints that back the service. You can configure the service selector to direct traffic through one route to multiple services. You can also create either unsecured or secured routes by using the TLS certificate that is assigned by the router for your hostname. Note that the router supports only the HTTP and HTTPS protocols.

[NodePort](/docs/openshift?topic=openshift-nodeport)
:   When you expose apps with a NodePort service, a NodePort in the range of 30000 - 32767 and an internal cluster IP address is assigned to the service. To access the service from outside the cluster, you use the public or private IP address of any worker node and the NodePort in the format `<IP_address>:<nodeport>`. However, the public and private IP addresses of the worker node are not permanent. When a worker node is removed or re-created, a new public and a new private IP address are assigned to the worker node. NodePorts are ideal for testing public or private access or providing access for only a short amount of time.

LoadBalancer
:   The LoadBalancer service type is implemented differently depending on your cluster's infrastructure provider.
    - **Classic clusters**: [Network load balancer (NLB)](/docs/openshift?topic=openshift-loadbalancer). Every standard cluster is provisioned with four portable public and four portable private IP addresses that you can use to create a layer 4 TCP/UDP network load balancer (NLB) for your app. You can customize your NLB by exposing any port that your app requires. The portable public and private IP addresses that are assigned to the NLB are permanent and do not change when a worker node is re-created in the cluster. If you create public NLBs, you can create a subdomain for your app that registers the public NLB IP addresses with a DNS entry. You can also enable health check monitors on the NLB IPs for each subdomain.
    - **VPC clusters**: [Load Balancer for VPC](/docs/openshift?topic=openshift-vpc-lbaas). When you create a Kubernetes LoadBalancer service for an app in your cluster, a layer 7 VPC load balancer is automatically created in your VPC outside of your cluster. The VPC load balancer is multizonal and routes requests for your app through the private NodePorts that are automatically opened on your worker nodes. By default, the load balancer is also created with a hostname that you can use to access your app, but you can also create a subdomain for your app that creates a DNS entry.
    


Ingress
:   <img src="images/icon-version-43.png" alt="Version 4 icon" width="30" style="width:30px; border-style: none"/> **{{site.data.keyword.openshiftshort}} version 4 clusters**: Expose multiple apps in a cluster by setting up routing with the [{{site.data.keyword.openshiftshort}} Ingress controller](/docs/openshift?topic=openshift-ingress-roks4). The Ingress controller uses the Ingress subdomain as a secured and unique public or private entry point to route incoming requests. You can use one subdomain to expose multiple apps in your cluster as services. Ingress consists of three components.

    - The Ingress controller is a HAProxy-based Kubernetes service that manages all incoming traffic for the apps in your cluster by implementing routing rules for the apps. This controller is managed by the Ingress operator.
    - The router listens for incoming HTTP, HTTPS, or TCP service requests, and then forwards requests to the pods for that app only according to the rules defined in the Ingress resource and implemented by the Ingress controller.
    - The Ingress resource defines the rules for how to route and load balance incoming requests for an app.

## Choosing among load balancing solutions
{: #routes-vs-ingress}

Now that you understand what [options](#external) you have to expose apps in your {{site.data.keyword.openshiftshort}} cluster, choose the best solution for your workload.
{: shortdesc}

**Do I use {{site.data.keyword.openshiftshort}} routes or Ingress?**

Because routes and Ingress offer similar capabilities, both load balancing solutions might be suitable to your workload. To help decide between routes and Ingress, consider the following broader concerns.
* **Portability across clouds**: If you anticipate running the same app in {{site.data.keyword.openshiftshort}} clusters in a hybrid scenario across multiple cloud providers, use the {{site.data.keyword.openshiftshort}} router. Routes are configured and work the same way across cloud providers, whereas Ingress might vary with each provider.
* **Annotations to extend routing capabilities**: With the Ingress ALB, you can customize Ingress routing rules with annotations. Some of these annotations help to integrate other {{site.data.keyword.cloud_notm}} services to your routes, such as {{site.data.keyword.appid_short}} to provide authentication for the Ingress URL that is assigned to your app. These annotations are not available for the {{site.data.keyword.openshiftshort}} router, which must use [route-specific `haproxy` annotations](https://docs.openshift.com/container-platform/4.7/networking/routes/route-configuration.html#nw-route-specific-annotations_route-configuration){: external}.

The following table compares the features of each app exposure method.

|Characteristics|NodePort|LoadBalancer (Classic - NLB)|LoadBalancer (VPC load balancer)|Ingress controller|Route|
|---------------|------|--------|---|-----------|
|Stable external IP| |Yes| |Yes|Yes|
|External hostname| |Yes|Yes|Yes|Yes|
|SSL termination| |Yes*|Yes*|Yes|Yes|
|HTTP(S) load balancing| | | |Yes|Yes|
|Custom routing rules| | | |Yes|Yes|
|Multiple apps per route or service| | | |Yes|Yes|
|{{site.data.keyword.cloud_notm}} extensions like {{site.data.keyword.appid_short}}| | | |Yes| |
|Consistent hybrid multicloud deployment| | | | |Yes|
{: caption="Comparison of external networking for apps in {{site.data.keyword.openshiftshort}} version 4 clusters." caption-side="top"}
{: #roks-net-compare-43}



|Characteristics|NodePort|NLB|Ingress ALB|Route|
|---------------|--------|---|-----------|-----|
|Stable external IP| |Yes|Yes|Yes|
|External hostname||Yes|Yes|Yes|
|HTTP(S) load balancing| |Yes*|Yes|Yes|
|TLS termination| | |Yes|Yes|
|Custom routing rules|| |Yes|Yes|
|Multiple apps per route or service| | |Yes|Yes|
|{{site.data.keyword.cloud_notm}} extensions like {{site.data.keyword.appid_short}}| | |Yes| |
|Consistent hybrid multicloud deployment| | | |Yes|
{: caption="Comparison of external networking for apps in {{site.data.keyword.openshiftshort}} version 3.11 clusters." caption-side="top"}
{: #roks-net-compare-311}



`*` SSL termination is provided by `ibmcloud oc nlb-dns` commands. In classic clusters, these commands are supported for public NLBs only.
{: note}



## Planning public external load balancing
{: #openshift_routers}

Publicly expose an app in your cluster to the internet.
{: shortdesc}

In ![Classic infrastructure provider icon.](images/icon-classic-2.svg) **classic** clusters, your worker nodes are connected to a public VLAN. The public VLAN determines the public IP address that is assigned to each worker node, which provides each worker node with a public network interface. Public networking services connect to this public network interface by providing your app with a public IP address and, optionally, a public URL.

In ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) **VPC** clusters, your worker nodes are connected to private VPC subnets only. However, when you create public networking services, a VPC load balancer is automatically created. The VPC load balancer can route public requests to your app by providing your app a public URL. When an app is publicly exposed, anyone that has the public URL can send a request to your app.

When an app is publicly exposed, anyone that has the public service IP address or the URL that you set up for your app can send a request to your app. For this reason, expose as few apps as possible. Expose an app to the public only when your app is ready to accept traffic from external web clients or users.

The public network interface for worker nodes is protected by [predefined Calico network policy settings](/docs/openshift?topic=openshift-network_policies#default_policy) that are configured on every worker node during cluster creation. By default, all outbound network traffic is allowed for all worker nodes. Inbound network traffic is blocked except for a few ports. These ports are opened so that IBM can monitor network traffic and automatically install security updates for the Kubernetes master, and so that connections can be established to public networking services. For more information about these policies, including how to modify them, see [Network policies](/docs/openshift?topic=openshift-network_policies#network_policies).

### Public app networking for classic clusters
{: #pattern_public}

![Classic infrastructure provider icon.](images/icon-classic-2.svg) To make an app publicly available to the internet in a classic cluster, choose an app exposure method that uses routes, NodePorts, NLBs, or setting up Ingress. The following table describes each possible method, why you might use it, and how to set it up. For basic information about the networking services that are listed, see [Understanding Kubernetes service types](#external).
{: shortdesc}

You cannot use multiple app exposure methods for one app.
{: note}


| Name | Load-balancing method | Use case | Implementation | 
| --- | --- | --- | --- |
| Route | HTTP(S) load balancing that exposes the app with a subdomain and uses custom routing rules | Implement custom routing rules and SSL termination for multiple apps. Choose this method to remain {{site.data.keyword.openshiftshort}}-native; for example, you can use the {{site.data.keyword.openshiftshort}} web console to create and manage routes.  \n 1. [Create a <code>ClusterIP</code> service](https://kubernetes.io/docs/concepts/services-networking/service/#defining-a-service){: external} to assign an internal IP address to your app.  \n 2. [Set up an {{site.data.keyword.openshiftshort}} route](https://docs.openshift.com/container-platform/4.7/applications/deployments/route-based-deployment-strategies.html){: external}.  \n 3. Customize routing rules with [optional configurations](https://docs.openshift.com/container-platform/4.7/networking/routes/route-configuration.html){: external}. |
| NodePort | Port on a worker node that exposes the app on the worker's public IP address | Test public access to one app or provide access for only a short amount of time. | [Create a public NodePort service](/docs/openshift?topic=openshift-nodeport#nodeport_config). |
| NLB v1.0 (+ subdomain) | Basic load balancing that exposes the app with an IP address or a subdomain. | Quickly expose one app to the public with an IP address or a subdomain that supports SSL termination. | [Create a public network load balancer](/docs/openshift?topic=openshift-loadbalancer#lb_config) (NLB) 1.0 in a [single](/docs/openshift?topic=openshift-loadbalancer#lb_config) or [multizone](/docs/openshift?topic=openshift-loadbalancer#multi_zone_config) cluster. Optionally [register](/docs/openshift?topic=openshift-loadbalancer_hostname) a subdomain and health checks. |
| NLB v2.0 (+ subdomain) | DSR load balancing that exposes the app with an IP address or a subdomain. | Expose an app that might receive high levels of traffic to the public with an IP address or a subdomain that supports SSL termination.  \n 1. Complete the [prerequisites](/docs/openshift?topic=openshift-loadbalancer-v2#ipvs_provision).  \n 2. Create a public NLB 2.0 in a [single](/docs/openshift?topic=openshift-loadbalancer-v2#ipvs_single_zone_config) or [multizone](/docs/openshift?topic=openshift-loadbalancer-v2#ipvs_multi_zone_config) cluster.  \n 3. Optionally [register](/docs/openshift?topic=openshift-loadbalancer_hostname) a subdomain and health checks. |
| {{site.data.keyword.openshiftshort}} version 4 clusters: Ingress controller | HTTP(S) load balancing that exposes the app with a subdomain and uses custom routing rules | Implement custom routing rules and SSL termination for multiple apps. | Create an [Ingress resource](/docs/openshift?topic=openshift-ingress-roks4#ingress-roks4-public). for the default public Ingress controller. | 
{: caption="Characteristics of public app exposure methods"}
{: summary="This table reads left to right about the name, characteristics, use cases, and deployment steps of public network deployment patterns."}

### Public app networking for VPC clusters
{: #pattern_public_vpc}

![VPC infrastructure provider icon.](images/icon-vpc-2.svg) To make an app publicly available to the internet in a VPC cluster, choose an app exposure method that uses routes, VPC load balancers, or setting up Ingress. The following table describes each possible method, why you might use it, and how to set it up. For basic information about the networking services that are listed, see [Understanding Kubernetes service types](#external).
{: shortdesc}

You cannot use multiple app exposure methods for one app.
{: note}

| Name | Load-balancing method | Use case | Implementation |
| --- | --- | --- | --- |
| Route | HTTP(S) load balancing that exposes the app with a subdomain and uses custom routing rules | Implement custom routing rules and SSL termination for multiple apps. Choose this method to remain {{site.data.keyword.openshiftshort}}-native; for example, you can use the {{site.data.keyword.openshiftshort}} web console to create and manage routes. | [Create a route](/docs/openshift?topic=openshift-openshift_routes#routes-public-classic) by using the default public router in clusters with a public cloud service endpoint, or [create a route](/docs/openshift?topic=openshift-openshift_routes#routes-public-vpc-privse) by using a custom public router in clusters with a private cloud service endpoint only. | 
| VPC load balancer | Basic load balancing that exposes the app with a hostname. | Quickly expose one app to the public with a VPC load balancer-assigned hostname. | [Create a public `LoadBalancer` service](/docs/openshift?topic=openshift-vpc-lbaas){: external} in your cluster. A multizonal VPC load balancer is automatically created in your VPC that assigns a hostname to your `LoadBalancer`service for your app. | 
| {{site.data.keyword.openshiftshort}} version 4 clusters: Ingress controller | HTTP(S) load balancing that exposes the app with a subdomain and uses custom routing rules. | Implement custom routing rules and SSL termination for multiple apps. | [Create an Ingress resource](/docs/openshift?topic=openshift-ingress-roks4#ingress-roks4-public) for the default public Ingress controller in clusters with a public cloud service endpoint, or [create an Ingress resource](/docs/openshift?topic=openshift-ingress-roks4#priv-se-pub-controller) for a custom public Ingress controller in clusters with a private cloud service endpoint only. | 
{: caption="Characteristics of public app exposure methods"}
{: summary="This table reads left to right about the name, characteristics, use cases, and deployment steps of public network deployment patterns."}



## Planning private external load balancing
{: #private_access}

Privately expose an app in your cluster to the private network only.
{: shortdesc}

When you deploy an app in a Kubernetes cluster in {{site.data.keyword.containerlong_notm}}, you might want to make the app accessible to only users and services that are on the same private network as your cluster. Private load balancing is ideal for making your app available to requests from outside the cluster without exposing the app to the general public. You can also use private load balancing to test access, request routing, and other configurations for your app before you later expose your app to the public with public network services.

As an example, say that you create a private load balancer for your app. This private load balancer can be accessed by:
* Any pod in that same cluster.
* Any pod in any cluster in the same {{site.data.keyword.cloud_notm}} account.
* If you're not in the {{site.data.keyword.cloud_notm}} account but still behind the company firewall, any system through a VPN connection to the subnet that the load balancer IP is on.
* If you're in a different {{site.data.keyword.cloud_notm}} account, any system through a VPN connection to the subnet that the load balancer IP is on.
* In classic clusters, if you have [VRF or VLAN spanning](/docs/openshift?topic=openshift-subnets#basics_segmentation) enabled, any system that is connected to any of the private VLANs in the same {{site.data.keyword.cloud_notm}} account.
* In VPC clusters:
    * If traffic is permitted between VPC subnets, any system in the same VPC.
    * If traffic is permitted between VPCs, any system that has access to the VPC that the cluster is in.

### Private app networking for classic clusters
{: #private_both_vlans}

![Classic infrastructure provider icon.](images/icon-classic-2.svg) When your worker nodes are connected to both a public and a private VLAN, you can make your app accessible from a private network only by creating private routes, NodePorts, NLBs, or setting up Ingress. Then, you can create Calico policies to block public traffic to the services.
{: shortdesc}

The public network interface for worker nodes is protected by [predefined Calico network policy settings](/docs/openshift?topic=openshift-network_policies#default_policy) that are configured on every worker node during cluster creation. By default, all outbound network traffic is allowed for all worker nodes. Inbound network traffic is blocked except for a few ports. These ports are opened so that IBM can monitor network traffic and automatically install security updates for the Kubernetes master, and so that connections can be established to NodePort, LoadBalancer, and Ingress services.

Because the default Calico network policies allow inbound public traffic to these services, you can create Calico policies to instead block all public traffic to the services. For example, a NodePort service opens a port on a worker node over both the private and public IP address of the worker node. An NLB service with a portable private IP address opens a public NodePort on every worker node. You must create a [Calico preDNAT network policy](/docs/openshift?topic=openshift-network_policies#block_ingress) to block public NodePorts.

Check out the following methods for private app networking:

|Name|Load-balancing method|Use case|Implementation|
|----|---------------------|--------|--------------|
| Route | HTTP(S) load balancing that exposes the app with a subdomain and uses custom routing rules|Implement custom routing rules and SSL termination for multiple apps. Choose this method to remain {{site.data.keyword.openshiftshort}}-native; for example, you can use the {{site.data.keyword.openshiftshort}} web console to create and manage routes.|  \n 1. [Create a `ClusterIP` service](https://kubernetes.io/docs/concepts/services-networking/service/#defining-a-service){: external} to assign an internal IP address to your app.  \n 2. [Create a router](/docs/openshift?topic=openshift-openshift_routes#private-routes-setup-43) that is exposed by a private load balancer.  \n 3. [Set up an {{site.data.keyword.openshiftshort}} route](https://docs.openshift.com/container-platform/4.7/applications/deployments/route-based-deployment-strategies.html){: external}.  \n 4. Customize routing rules with [optional configurations](https://docs.openshift.com/container-platform/4.7/networking/routes/route-configuration.html){: external}. |
| NodePort | Port on a worker node that exposes the app on the worker's private IP address|Test private access to one app or provide access for only a short amount of time.|  \n 1. [Create a NodePort service](/docs/openshift?topic=openshift-nodeport).  \n 2. A NodePort service opens a port on a worker node over both the private and public IP address of the worker node. You must use a [Calico preDNAT network policy](/docs/openshift?topic=openshift-network_policies#block_ingress) to block traffic to the public NodePorts. |
| NLB 1.0 | Basic load balancing that exposes the app with a private IP address|Quickly expose one app to a private network with a private IP address.|  \n 1. [Create a private NLB service](/docs/openshift?topic=openshift-loadbalancer). An NLB with a portable private IP address still has a public node port open on every worker node.  \n 2. Create a [Calico preDNAT network policy](/docs/openshift?topic=openshift-network_policies#block_ingress) to block traffic to the public NodePorts. |
| NLB v2.0 | DSR load balancing that exposes the app with a private IP address|Expose an app that might receive high levels of traffic to a private network with an IP address.|  \n 1. Complete the [prerequisites](/docs/openshift?topic=openshift-loadbalancer-v2#ipvs_provision).  \n 2. Create a private NLB 2.0 in a [single](/docs/openshift?topic=openshift-loadbalancer-v2#ipvs_single_zone_config) or [multizone](/docs/openshift?topic=openshift-loadbalancer-v2#ipvs_multi_zone_config) cluster. An NLB with a portable private IP address still has a public node port open on every worker node.  \n 3. Create a [Calico preDNAT network policy](/docs/openshift?topic=openshift-network_policies#block_ingress) to block traffic to the public NodePorts. |
| {{site.data.keyword.openshiftshort}} version 4 clusters: Ingress controller |HTTP(S) load balancing that exposes the app with a subdomain and uses custom routing rules|Implement custom routing rules and SSL termination for multiple apps.|  \n 1. [Register your custom domain](/docs/openshift?topic=openshift-ingress-roks4#ingress-roks4-private-2).  \n 2. [Create and configure a private Ingress controller](/docs/openshift?topic=openshift-ingress-roks4#ingress-roks4-private-3).  \n 3. Create an [Ingress resource](/docs/openshift?topic=openshift-ingress-roks4#ingress-roks4-private-4) for the private Ingress controller. |
{: caption="Characteristics of network deployment patterns for a public and a private VLAN setup" caption-side="top"}



### Private app networking for VPC clusters
{: #private_vpc}

![VPC infrastructure provider icon.](images/icon-vpc-2.svg) To make an app available over a private network only in a VPC cluster, choose a load balancing deployment pattern based on your cluster's service endpoint setup: public and private cloud service endpoint, or private cloud service endpoint only. For each service endpoint setup, the following table describes each possible app exposure method, why you might use it, and how to set it up.
{: shortdesc}

<img src="images/icon-version-43.png" alt="Version 4 icon" width="30" style="width:30px; border-style: none"/> Only version 4 clusters can be created on VPC infrastructure. The following methods do not apply to version 3.11 clusters, which can be created on classic infrastructure only.</br></br>You cannot use multiple app exposure methods for one app.
{: note}

|Name|Load-balancing method|Use case|Implementation|
|----|---------------------|--------|--------------|
|Route|HTTP(S) load balancing that exposes the app with a subdomain and uses custom routing rules|Implement custom routing rules and SSL termination for multiple apps. Choose this method to remain {{site.data.keyword.openshiftshort}}-native; for example, you can use the {{site.data.keyword.openshiftshort}} web console to create and manage routes.|[Create a route by using the default private router in clusters with a private cloud service endpoint only](/docs/openshift?topic=openshift-openshift_routes#private-routes-setup-43), or [create a route by using a custom private router in clusters with a public cloud service endpoint](/docs/openshift?topic=openshift-openshift_routes#routes-private-vpc-privse).|
|NodePort|Port on a worker node that exposes the app on the worker's private IP address|Test private access to one app or provide access for only a short amount of time.|[Create a private NodePort service](/docs/openshift?topic=openshift-nodeport).|
|VPC load balancer|Basic load balancing that exposes the app with a private hostname|Quickly expose one app to a private network with a VPC load balancer-assigned private hostname.|[Create a private `LoadBalancer` service](/docs/openshift?topic=openshift-vpc-lbaas) in your cluster. A multizonal VPC load balancer is automatically created in your VPC that assigns a hostname to your `LoadBalancer` service for your app.|
|Ingress controller|HTTP(S) load balancing that exposes the app with a subdomain and uses custom routing rules|Implement custom routing rules and SSL termination for multiple apps.|[Create an Ingress resource for the default private Ingress controller in clusters with a private cloud service endpoint only](/docs/openshift?topic=openshift-ingress-roks4#priv-se-priv-controller), or [create an Ingress resource for a custom private Ingress controller in clusters with a public cloud service endpoint](/docs/openshift?topic=openshift-ingress-roks4#ingress-roks4-private).|
{: caption="Private network deployment patterns for a VPC cluster" caption-side="top"}






