---

copyright:
  years: 2014, 2025
lastupdated: "2025-08-13"


keywords: openshift, networking

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}




# Choosing an app exposure service
{: #cs_network_planning}

Securely expose your apps to external traffic by using {{site.data.keyword.redhat_openshift_notm}} Ingress controller or {{site.data.keyword.containerlong}} NodePort, or network load balancer.
{: shortdesc}

## Understanding options for exposing apps
{: #external}

To securely expose your apps to external traffic, you can use choose from the following services.
{: shortdesc}

[{{site.data.keyword.redhat_openshift_notm}} Ingress controller](/docs/openshift?topic=openshift-openshift_routes)
:   Expose multiple apps in a cluster by setting up routing with the {{site.data.keyword.redhat_openshift_notm}} Ingress controller. The Ingress controller uses the Ingress subdomain as a secured and unique public or private entry point to route incoming requests. You can use one subdomain to expose multiple apps in your cluster as services. The Ingress controller solution uses three components.

    - The Ingress operator that manages the Ingress controllers in your cluster. 
    - The Ingress controller is a HAProxy-based Kubernetes service that manages all incoming traffic for the apps in your cluster by implementing routing rules for the apps. This controller is managed by the Ingress operator. The Ingress controller listens for incoming HTTP, or HTTPS service requests, and then forwards requests to the pods for that app only according to the rules defined in the Ingress resource and implemented by the Ingress controller.
    - The Route resource defines the rules for how to route and load balance incoming requests for an app.

:   A Route exposes a service as a hostname in the format `<service_name>-<project>.<cluster_name>-<random_hash>-0000.<region>.containers.appdomain.cloud`. An Ingress controller is deployed by default to your cluster, which enable Routes to be used by external clients. The Ingress controller uses the service selector to find the service and the endpoints that back the service. You can configure the service selector to direct traffic through one Route to multiple services. You can also create either unsecured or secured Routes by using the TLS certificate that is assigned by the Ingress controller for your hostname. Note that the Ingress controller supports only the HTTP and HTTPS protocols.

[NodePort](/docs/openshift?topic=openshift-nodeport)
:   When you expose apps with a NodePort service, a NodePort in the range of 30000 - 32767 and an internal cluster IP address is assigned to the service. To access the service from outside the cluster, you use the public or private IP address of any worker node and the NodePort in the format `<IP_address>:<nodeport>`. However, the public and private IP addresses of the worker node are not permanent. When a worker node is removed or re-created, a new public and a new private IP address are assigned to the worker node. NodePorts are ideal for testing public or private access or providing access for only a short amount of time.

LoadBalancer
:   The LoadBalancer service type is implemented differently depending on your cluster's infrastructure provider.
    - **Classic clusters**: [Network load balancer (NLB)](/docs/openshift?topic=openshift-loadbalancer). Every standard cluster is provisioned with four portable public and four portable private IP addresses that you can use to create a layer 4 TCP/UDP network load balancer (NLB) for your app. You can customize your NLB by exposing any port that your app requires. The portable public and private IP addresses that are assigned to the NLB are permanent and don't change when a worker node is re-created in the cluster. If you create public NLBs, you can create a subdomain for your app that registers the public NLB IP addresses with a DNS entry. You can also enable health check monitors on the NLB IPs for each subdomain.
    - **VPC clusters**: [Load Balancer for VPC](/docs/openshift?topic=openshift-vpclb-about). When you create a Kubernetes LoadBalancer service for an app in your cluster, a layer 7 VPC load balancer is automatically created in your VPC outside of your cluster. The VPC load balancer is multizonal and routes requests for your app through the private NodePorts that are automatically opened on your worker nodes. By default, the load balancer is also created with a hostname that you can use to access your app, but you can also create a subdomain for your app that creates a DNS entry.
    


Ingress
:   You can use [Ingress](/docs/openshift?topic=openshift-ingress-roks4) to expose your app to external traffic via the {{site.data.keyword.redhat_openshift_notm}} Ingress controller. The {{site.data.keyword.redhat_openshift_notm}} Controller Manager converts your Ingress resources to Route resources and the {{site.data.keyword.redhat_openshift_notm}} Ingress controller processes those Routes.

## Choosing among load balancing solutions
{: #load-balancing-comparison}

Now that you understand what [options](#external) you have to expose apps in your {{site.data.keyword.redhat_openshift_notm}} cluster, choose the best solution for your workload.
{: shortdesc}

The following table compares the features of each app exposure method.

|Characteristics| NodePort | LoadBalancer (Classic - NLB)| LoadBalancer (VPC load balancer) |Ingress controller|
| --- | --- | --- | --- | --- |
|Stable external IP| |Yes| |Yes|
|External hostname| |Yes|Yes|Yes|
|SSL termination| |Yes*|Yes*|Yes|
|HTTP(S) load balancing| | | |Yes|
|Custom routing rules| | | |Yes|
|Multiple apps per route or service| | | |Yes|
|Consistent hybrid multicloud deployment| | | |Yes|
{: #roks-net-compare-43}
{: caption="Comparison of external networking for apps in {{site.data.keyword.redhat_openshift_notm}} clusters." caption-side="bottom"}




`*` SSL termination is provided by `ibmcloud oc nlb-dns` commands. In classic clusters, these commands are supported for public NLBs only.
{: note}



## Planning public external load balancing
{: #openshift_routers}

Publicly expose an app in your cluster to the internet.
{: shortdesc}

In **classic** clusters, your worker nodes are connected to a public VLAN. The public VLAN determines the public IP address that is assigned to each worker node, which provides each worker node with a public network interface. Public networking services connect to this public network interface by providing your app with a public IP address and, optionally, a public URL.

In **VPC** clusters, your worker nodes are connected to private VPC subnets only. However, when you create public networking services, a VPC load balancer is automatically created. The VPC load balancer can route public requests to your app by providing your app a public URL. When an app is publicly exposed, anyone that has the public URL can send a request to your app.

When an app is publicly exposed, anyone that has the public service IP address or the URL that you set up for your app can send a request to your app. For this reason, expose as few apps as possible. Expose an app to the public only when your app is ready to accept traffic from external web clients or users.

The public network interface for worker nodes is protected by [predefined Calico network policy settings](/docs/openshift?topic=openshift-network_policies#default_policy) that are configured on every worker node during cluster creation. By default, all outbound network traffic is allowed for all worker nodes. Inbound network traffic is blocked except for a few ports. These ports are opened so that IBM can monitor network traffic and automatically install security updates for the Kubernetes master, and so that connections can be established to public networking services. For more information about these policies, including how to modify them, see [Network policies](/docs/openshift?topic=openshift-network_policies#network_policies).

### Public app networking for classic clusters
{: #pattern_public}

To make an app publicly available to the internet in a classic cluster, choose an app exposure method that uses routes, NodePorts, NLBs, or setting up Ingress. The following table describes each possible method, why you might use it, and how to set it up. For basic information about the networking services that are listed, see [Understanding Kubernetes service types](#external).
{: shortdesc}

You can't use multiple app exposure methods for one app.
{: note}


| Name | Load-balancing method | Use case | Implementation | 
| --- | --- | --- | --- |
| Route | HTTP(S) load balancing that exposes the app with a subdomain and uses custom routing rules | Implement custom routing rules and SSL termination for multiple apps. Choose this method to remain {{site.data.keyword.redhat_openshift_notm}}-native; for example, you can use the {{site.data.keyword.redhat_openshift_notm}} web console to create and manage routes.  \n 1. [Create a `ClusterIP` service](https://kubernetes.io/docs/concepts/services-networking/service/#defining-a-service){: external} to assign an internal IP address to your app.  \n 2. [Set up a {{site.data.keyword.redhat_openshift_notm}} route](https://docs.openshift.com/container-platform/4.18/applications/deployments/route-based-deployment-strategies.html){: external}.  \n 3. Customize routing rules with [optional configurations](https://docs.redhat.com/en/documentation/openshift_container_platform/4.18/html/ingress_and_load_balancing/configuring-routes){: external}. |
| NodePort | Port on a worker node that exposes the app on the worker's public IP address | Test public access to one app or provide access for only a short amount of time. | [Create a public NodePort service](/docs/openshift?topic=openshift-nodeport#nodeport_config). |
| NLB v1.0 (+ subdomain) | Basic load balancing that exposes the app with an IP address or a subdomain. | Quickly expose one app to the public with an IP address or a subdomain that supports SSL termination. | [Create a public network load balancer](/docs/openshift?topic=openshift-loadbalancer#lb_config) (NLB) 1.0 in a [single](/docs/openshift?topic=openshift-loadbalancer#lb_config) or [multizone](/docs/openshift?topic=openshift-loadbalancer#multi_zone_config) cluster. Optionally [register](/docs/openshift?topic=openshift-loadbalancer_hostname) a subdomain and health checks. |
| NLB v2.0 (+ subdomain) | DSR load balancing that exposes the app with an IP address or a subdomain. | Expose an app that might receive high levels of traffic to the public with an IP address or a subdomain that supports SSL termination.  \n 1. Complete the [prerequisites](/docs/openshift?topic=openshift-loadbalancer-v2#ipvs_provision).  \n 2. Create a public NLB 2.0 in a [single](/docs/openshift?topic=openshift-loadbalancer-v2#ipvs_single_zone_config) or [multizone](/docs/openshift?topic=openshift-loadbalancer-v2#ipvs_multi_zone_config) cluster.  \n 3. Optionally [register](/docs/openshift?topic=openshift-loadbalancer_hostname) a subdomain and health checks. |
| Ingress controller | HTTP(S) load balancing that exposes the app with a subdomain and uses custom routing rules | Implement custom routing rules and SSL termination for multiple apps. | Create an [Ingress resource](/docs/openshift?topic=openshift-ingress-public-expose&interface=ui). for the default public Ingress controller. | 
{: caption="Characteristics of public app exposure methods"}


### Public app networking for VPC clusters
{: #pattern_public_vpc}

To make an app publicly available to the internet in a VPC cluster, choose an app exposure method that uses routes, VPC load balancers, or setting up Ingress. The following table describes each possible method, why you might use it, and how to set it up. For basic information about the networking services that are listed, see [Understanding Kubernetes service types](#external).
{: shortdesc}

You can't use multiple app exposure methods for one app.
{: note}



| Name | Load-balancing method | Use case | Implementation |
| --- | --- | --- | --- |
| Route | HTTP(S) load balancing that exposes the app with a subdomain and uses custom routing rules | Implement custom routing rules and SSL termination for multiple apps. Choose this method to remain {{site.data.keyword.redhat_openshift_notm}}-native; for example, you can use the {{site.data.keyword.redhat_openshift_notm}} web console to create and manage routes. | [Create a route](/docs/openshift?topic=openshift-openshift_routes#routes-public-classic) by using the default public Ingress controller in clusters with a public cloud service endpoint, or [create a route](/docs/openshift?topic=openshift-openshift_routes#routes-public-vpc-privse) by using a custom public Ingress controller in clusters with a private cloud service endpoint only. | 
| VPC load balancer | Basic load balancing that exposes the app with a hostname. | Quickly expose one app to the public with a VPC load balancer-assigned hostname. | [Create a public `LoadBalancer` service](/docs/openshift?topic=openshift-vpclb-about){: external} in your cluster. A multizonal VPC load balancer is automatically created in your VPC that assigns a hostname to your `LoadBalancer`service for your app. | 
| Ingress | HTTP(S) load balancing that exposes the app with a subdomain and uses custom routing rules. | Implement custom routing rules and SSL termination for multiple apps. | [Create an Ingress resource](/docs/openshift?topic=openshift-ingress-public-expose&interface=ui#ingress-public-se) for the default public Ingress controller in clusters with a public cloud service endpoint, or [create an Ingress resource](/docs/openshift?topic=openshift-ingress-public-expose#ingress-public-expose-vpc-private-se) for a custom public Ingress controller in clusters with a private cloud service endpoint only. | 
{: caption="Characteristics of public app exposure methods"}




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

When your worker nodes are connected to both a public and a private VLAN, you can make your app accessible from a private network only by creating private routes, NodePorts, NLBs, or setting up Ingress. Then, you can create Calico policies to block public traffic to the services.
{: shortdesc}

The public network interface for worker nodes is protected by [predefined Calico network policy settings](/docs/openshift?topic=openshift-network_policies#default_policy) that are configured on every worker node during cluster creation. By default, all outbound network traffic is allowed for all worker nodes. Inbound network traffic is blocked except for a few ports. These ports are opened so that IBM can monitor network traffic and automatically install security updates for the Kubernetes master, and so that connections can be established to NodePort, LoadBalancer, and Ingress services.

Because the default Calico network policies allow inbound public traffic to these services, you can create Calico policies to instead block all public traffic to the services. For example, a NodePort service opens a port on a worker node over both the private and public IP address of the worker node. An NLB service with a portable private IP address opens a public NodePort on every worker node. You must create a [Calico preDNAT network policy](/docs/openshift?topic=openshift-network_policies#block_ingress) to block public NodePorts.

Check out the following methods for private app networking:

|Name|Load-balancing method|Use case|Implementation|
|----|---------------------|--------|--------------|
| Route | HTTP(S) load balancing that exposes the app with a subdomain and uses custom routing rules|Implement custom routing rules and SSL termination for multiple apps. Choose this method to remain {{site.data.keyword.redhat_openshift_notm}}-native; for example, you can use the {{site.data.keyword.redhat_openshift_notm}} web console to create and manage routes.|  \n 1. [Create a `ClusterIP` service](https://kubernetes.io/docs/concepts/services-networking/service/#defining-a-service){: external} to assign an internal IP address to your app.  \n 2. [Create an Ingress controller](/docs/openshift?topic=openshift-openshift_routes#private-routes-setup-43) that is exposed by a private load balancer.  \n 3. [Set up a {{site.data.keyword.redhat_openshift_notm}} route](https://docs.openshift.com/container-platform/4.18/applications/deployments/route-based-deployment-strategies.html){: external}.  \n 4. Customize routing rules with [optional configurations](https://docs.redhat.com/en/documentation/openshift_container_platform/4.18/html/ingress_and_load_balancing/configuring-routes){: external}. |
| NodePort | Port on a worker node that exposes the app on the worker's private IP address|Test private access to one app or provide access for only a short amount of time.|  \n 1. [Create a NodePort service](/docs/openshift?topic=openshift-nodeport).  \n 2. A NodePort service opens a port on a worker node over both the private and public IP address of the worker node. You must use a [Calico preDNAT network policy](/docs/openshift?topic=openshift-network_policies#block_ingress) to block traffic to the public NodePorts. |
| NLB 1.0 | Basic load balancing that exposes the app with a private IP address|Quickly expose one app to a private network with a private IP address.|  \n 1. [Create a private NLB service](/docs/openshift?topic=openshift-loadbalancer). An NLB with a portable private IP address still has a public node port open on every worker node.  \n 2. Create a [Calico preDNAT network policy](/docs/openshift?topic=openshift-network_policies#block_ingress) to block traffic to the public NodePorts. |
| NLB v2.0 | DSR load balancing that exposes the app with a private IP address|Expose an app that might receive high levels of traffic to a private network with an IP address.|  \n 1. Complete the [prerequisites](/docs/openshift?topic=openshift-loadbalancer-v2#ipvs_provision).  \n 2. Create a private NLB 2.0 in a [single](/docs/openshift?topic=openshift-loadbalancer-v2#ipvs_single_zone_config) or [multizone](/docs/openshift?topic=openshift-loadbalancer-v2#ipvs_multi_zone_config) cluster. An NLB with a portable private IP address still has a public node port open on every worker node.  \n 3. Create a [Calico preDNAT network policy](/docs/openshift?topic=openshift-network_policies#block_ingress) to block traffic to the public NodePorts. |
| Ingress |HTTP(S) load balancing that exposes the app with a subdomain and uses custom routing rules|Implement custom routing rules and SSL termination for multiple apps.|  See [Publicly exposing apps with Ingress](/docs/openshift?topic=openshift-ingress-public-expose&interface=ui)|
{: caption="Characteristics of network deployment patterns for a public and a private VLAN setup" caption-side="bottom"}



### Private app networking for VPC clusters
{: #private_vpc}

To make an app available over a private network only in a VPC cluster, choose a load balancing deployment pattern based on your cluster's service endpoint setup: public and private cloud service endpoint, or private cloud service endpoint only. For each service endpoint setup, the following table describes each possible app exposure method, why you might use it, and how to set it up.
{: shortdesc}


|Name|Load-balancing method|Use case|Implementation|
|----|---------------------|--------|--------------|
|Route|HTTP(S) load balancing that exposes the app with a subdomain and uses custom routing rules|Implement custom routing rules and SSL termination for multiple apps. Choose this method to remain {{site.data.keyword.redhat_openshift_notm}}-native; for example, you can use the {{site.data.keyword.redhat_openshift_notm}} web console to create and manage routes.|[Create an Ingress controller by using the default private Ingress controller in clusters with a private cloud service endpoint only](/docs/openshift?topic=openshift-openshift_routes#private-routes-setup-43), or [create a route by using a custom private Ingress controller in clusters with a public cloud service endpoint](/docs/openshift?topic=openshift-openshift_routes#routes-private-vpc-privse).|
|NodePort|Port on a worker node that exposes the app on the worker's private IP address|Test private access to one app or provide access for only a short amount of time.|[Create a private NodePort service](/docs/openshift?topic=openshift-nodeport).|
|VPC load balancer|Basic load balancing that exposes the app with a private hostname|Quickly expose one app to a private network with a VPC load balancer-assigned private hostname.|[Create a private `LoadBalancer` service](/docs/openshift?topic=openshift-vpclb-about) in your cluster. A multizonal VPC load balancer is automatically created in your VPC that assigns a hostname to your `LoadBalancer` service for your app.|
|Ingress|HTTP(S) load balancing that exposes the app with a subdomain and uses custom routing rules|Implement custom routing rules and SSL termination for multiple apps.|[Create an Ingress resource for the default private Ingress controller in clusters with a private cloud service endpoint only](/docs/openshift?topic=openshift-ingress-private-expose#priv-se-priv-controller), or [create an Ingress resource for a custom private Ingress controller in clusters with a public cloud service endpoint](/docs/openshift?topic=openshift-ingress-private-expose).|
{: caption="Private network deployment patterns for a VPC cluster" caption-side="bottom"}
