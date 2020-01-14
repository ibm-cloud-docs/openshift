---

copyright:
  years: 2014, 2020
lastupdated: "2020-01-14"

keywords: openshift, roks, rhoks, rhos, networking

subcollection: openshift

---

{:codeblock: .codeblock}
{:deprecated: .deprecated}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:gif: data-image-type='gif'}
{:help: data-hd-content-type='help'}
{:important: .important}
{:new_window: target="_blank"}
{:note: .note}
{:pre: .pre}
{:preview: .preview}
{:screen: .screen}
{:shortdesc: .shortdesc}
{:support: data-reuse='support'}
{:table: .aria-labeledby="caption"}
{:tip: .tip}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}


# Choosing an app exposure service
{: #cs_network_planning}

Securely expose your apps to external traffic by using OpenShift routes or {{site.data.keyword.containerlong}} NodePort, network load balancer, or Ingress application load balancer services.
{: shortdesc}

## Understanding options for exposing apps
{: #external}

To securely expose your apps to external traffic, you can use choose from the following services.
{: shortdesc}

<dl>
<dt>[OpenShift route ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/architecture/networking/routes.html)</dt>
<dd>A route exposes a service as a hostname in the format `<service_name>-<project>.<cluster_name>-<random_hash>-0001.<region>.containers.appdomain.cloud`. A router is deployed by default to your cluster, which enable routes to be used by external clients. The router uses the service selector to find the service and the endpoints that back the service. You can configure the service selector to direct traffic through one route to multiple services. You can also create either unsecured or secured routes by using the TLS certificate that is assigned by the router for your hostname. **Note**: The hostname that is assigned to your route is different than the Ingress subdomain that is assigned by default to your cluster. Your route does not use the Ingress subdomain.</dd>

<dt>[NodePort](/docs/openshift?topic=openshift-nodeport)</dt>
<dd>When you expose apps with a NodePort service, a NodePort in the range of 30000 - 32767 and an internal cluster IP address is assigned to the service. To access the service from outside the cluster, you use the public or private IP address of any worker node and the NodePort in the format <code>&lt;IP_address&gt;:&lt;nodeport&gt;</code>. However, the public and private IP addresses of the worker node are not permanent. When a worker node is removed or re-created, a new public and a new private IP address are assigned to the worker node. NodePorts are ideal for testing public or private access or providing access for only a short amount of time.</dd>

<dt>[Network load balancer (NLB)](/docs/openshift?topic=openshift-loadbalancer)</dt>
<dd>Every standard cluster is provisioned with four portable public and four portable private IP addresses that you can use to create a layer 4 TCP/UDP network load balancer (NLB) for your app. You can customize your NLB by exposing any port that your app requires. The portable public and private IP addresses that are assigned to the NLB are permanent and do not change when a worker node is re-created in the cluster. If you create public NLBs, you can create a subdomain for your app that registers the public NLB IP addresses with a DNS entry. You can also enable health check monitors on the NLB IPs for each subdomain.</dd>

<dt>[Ingress application load balancer (ALB)](/docs/openshift?topic=openshift-ingress)</dt>
<dd>Expose multiple apps in a cluster by setting up routing with the Ingress application load balancer (ALB). The ALB uses the Ingress subdomain as a secured and unique public or private entry point to route incoming requests. You can use one subdomain to expose multiple apps in your cluster as services. Ingress consists of three components:<ul>
  <li>The Ingress resource defines the rules for how to route and load balance incoming requests for an app.</li>
  <li>The ALB listens for incoming HTTP, HTTPS, or TCP service requests. It forwards requests across the apps' pods based on the rules that you defined in the Ingress resource, including custom routing rules defined by annotations.</li>
  <li>The multizone load balancer (MZLB) handles all incoming requests to your apps and load balances the requests among the ALBs in the various zones. It also enables health checks for the public Ingress IP addresses.</li></ul>Note that the Ingress system does not use the router that is deployed by default to your cluster, and that any routes you create do not use the Ingress subdomain.</dd>
</dl>

## Choosing among load balancing solutions
{: #routes-vs-ingress}

Now that you understand what [options](#external) you have to expose apps in your OpenShift cluster, choose the best solution for your workload.
{: shortdesc}

**Do I use OpenShift routes or Ingress?**<br>
Because routes and Ingress offer similar capabilities, both load balancing solutions might be suitable to your workload. To help decide between routes and Ingress, consider the following broader concerns.
* **Portability across clouds**: If you anticipate running the same app in OpenShift clusters in a hybrid scenario across multiple cloud providers, use the OpenShift router. Routes are configured and work the same way across cloud providers, whereas Ingress might vary with each provider.
* **Annotations to extend routing capabilities**: With the Ingress ALB, you can customize Ingress routing rules with annotations. Some of these annotations help to integrate other {{site.data.keyword.cloud_notm}} services to your routes, such as {{site.data.keyword.appid_short}} to provide authentication for the Ingress URL that is assigned to your app. These annotations are not available for the OpenShift router, which must use [route-specific `haproxy` annotations](https://docs.openshift.com/container-platform/3.11/architecture/networking/routes.html#route-specific-annotations){: external}.

The following table compares the features of each app exposure method.

|Characteristics|NodePort|NLB|Ingress ALB|Route|
|---------------|--------|---|-----------|-----|
|Stable external IP| |<img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" />|<img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" />|<img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" />|
|External hostname||<img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" />|<img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" />|<img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" />|
|HTTP(S) load balancing| |<img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" />*|<img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" />|<img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" />|
|TLS termination| | |<img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" />|<img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" />|
|Custom routing rules|| |<img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" />|<img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" />|
|Multiple apps per route or service| | |<img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" />|<img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" />|
|{{site.data.keyword.cloud_notm}} extensions like {{site.data.keyword.appid_short}}| | |<img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" />| |
|Consistent hybrid multicloud deployment| | | |<img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" />|
{: caption="Comparison of OpenShift external networking for apps" caption-side="top"}

`*` An SSL certificate for HTTPS load balancing is provided by `ibmcloud oc nlb-dns` commands. In classic clusters, these commands are supported for public NLBs only.
{: note}


<br />


## Planning public external load balancing
{: #openshift_routers}

Publicly expose an app in your cluster to the internet.
{: shortdesc}

You can connect worker nodes to a public VLAN. The public VLAN determines the public IP address that is assigned to each worker node, which provides each worker node with a public network interface. Public networking services connect to this public network interface by providing your app with a public IP address and, optionally, a public URL.

When an app is publicly exposed, anyone that has the public service IP address or the URL that you set up for your app can send a request to your app. For this reason, expose as few apps as possible. Expose an app to the public only when your app is ready to accept traffic from external web clients or users.

The public network interface for worker nodes is protected by [predefined Calico network policy settings](/docs/openshift?topic=openshift-network_policies#default_policy) that are configured on every worker node during cluster creation. By default, all outbound network traffic is allowed for all worker nodes. Inbound network traffic is blocked except for a few ports. These ports are opened so that IBM can monitor network traffic and automatically install security updates for the Kubernetes master, and so that connections can be established to public networking services. For more information about these policies, including how to modify them, see [Network policies](/docs/openshift?topic=openshift-network_policies#network_policies).

### Choosing an app exposure method
{: #pattern_public}

To make an app publicly available to the internet in a classic cluster, choose an app exposure method that uses routes, NodePorts, NLBs, or setting up Ingress. The following table describes each possible method, why you might use it, and how to set it up. For basic information about the networking services that are listed, see [Understanding Kubernetes service types](#external).
{: shortdesc}

You cannot use multiple app exposure methods for one app.
{: note}

<table summary="This table reads left to right about the name, characteristics, use cases, and deployment steps of public network deployment patterns.">
<caption>Characteristics of public app exposure methods in Red Hat OpenShift on IBM Cloud</caption>
<col width="10%">
<col width="25%">
<col width="25%">
<thead>
<th>Name</th>
<th>Load-balancing method</th>
<th>Use case</th>
<th>Implementation</th>
</thead>
<tbody>
<tr>
<td>Route</td>
<td>HTTP(S) load balancing that exposes the app with a subdomain and uses custom routing rules</td>
<td>Implement custom routing rules and SSL termination for multiple apps. Choose this method to remain OpenShift-native; for example, you can use the OpenShift web console to create and manage routes.</td>
<td><ol><li>[Create a `ClusterIP` service ![External link icon](../icons/launch-glyph.svg "External link icon")](https://kubernetes.io/docs/concepts/services-networking/service/#defining-a-service) to assign an internal IP address to your app.</li><li>[Set up an OpenShift route ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/dev_guide/routes.html).</li><li>Customize routing rules with [optional configurations ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/architecture/networking/routes.html).</li></ol></td>
</tr>
<tr>
<td>NodePort</td>
<td>Port on a worker node that exposes the app on the worker's public IP address</td>
<td>Test public access to one app or provide access for only a short amount of time.</td>
<td>[Create a public NodePort service](/docs/openshift?topic=openshift-nodeport#nodeport_config).</td>
</tr>
<tr>
<td>NLB v1.0 (+ subdomain)</td>
<td>Basic load balancing that exposes the app with an IP address or a subdomain</td>
<td>Quickly expose one app to the public with an IP address or a subdomain that supports SSL termination.</td>
<td><ol><li>Create a public network load balancer (NLB) 1.0 in a [single-](/docs/openshift?topic=openshift-loadbalancer#lb_config) or [multizone](/docs/openshift?topic=openshift-loadbalancer#multi_zone_config) cluster.</li><li>Optionally [register](/docs/openshift?topic=openshift-loadbalancer_hostname) a subdomain and health checks.</li></ol></td>
</tr>
<tr>
<td>NLB v2.0 (+ subdomain)</td>
<td>DSR load balancing that exposes the app with an IP address or a subdomain</td>
<td>Expose an app that might receive high levels of traffic to the public with an IP address or a subdomain that supports SSL termination.</td>
<td><ol><li>Complete the [prerequisites](/docs/openshift?topic=openshift-loadbalancer-v2#ipvs_provision).</li><li>Create a public NLB 2.0 in a [single-](/docs/openshift?topic=openshift-loadbalancer-v2#ipvs_single_zone_config) or [multizone](/docs/openshift?topic=openshift-loadbalancer-v2#ipvs_multi_zone_config) cluster.</li><li>Optionally [register](/docs/openshift?topic=openshift-loadbalancer_hostname) a subdomain and health checks.</li></ol></td>
</tr>
<tr>
<td>Ingress ALB</td>
<td>HTTP(S) load balancing that exposes the app with a subdomain and uses custom routing rules</td>
<td>Implement custom routing rules and SSL termination for multiple apps. Choose this method only if you have specific requirements to use Ingress instead of routes, such as migrating an app that already uses Ingress from a community Kubernetes cluster.</td>
<td><ol><li>Create an [Ingress resource](/docs/openshift?topic=openshift-ingress#ingress_expose_public) for the public ALB.</li><li>Customize ALB routing rules with [annotations](/docs/openshift?topic=openshift-ingress_annotation).</li></ol></td>
</tr>
</tbody>
</table>

<br />


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
* If you have [VRF or VLAN spanning](/docs/openshift?topic=openshift-subnets#basics_segmentation) enabled, any system that is connected to any of the private VLANs in the same {{site.data.keyword.cloud_notm}} account.

### Choosing an app exposure method
{: #private_both_vlans}

When your worker nodes are connected to both a public and a private VLAN, you can make your app accessible from a private network only by creating private routes, NodePorts, NLBs, or setting up Ingress. Then, you can create Calico policies to block public traffic to the services.
{: shortdesc}

The public network interface for worker nodes is protected by [predefined Calico network policy settings](/docs/openshift?topic=openshift-network_policies#default_policy) that are configured on every worker node during cluster creation. By default, all outbound network traffic is allowed for all worker nodes. Inbound network traffic is blocked except for a few ports. These ports are opened so that IBM can monitor network traffic and automatically install security updates for the Kubernetes master, and so that connections can be established to NodePort, LoadBalancer, and Ingress services.

Because the default Calico network policies allow inbound public traffic to these services, you can create Calico policies to instead block all public traffic to the services. For example, a NodePort service opens a port on a worker node over both the private and public IP address of the worker node. An NLB service with a portable private IP address opens a public NodePort on every worker node. You must create a [Calico preDNAT network policy](/docs/openshift?topic=openshift-network_policies#block_ingress) to block public NodePorts.

Check out the following methods for private app networking:

|Name|Load-balancing method|Use case|Implementation|
|----|---------------------|--------|--------------|
|Route|HTTP(S) load balancing that exposes the app with a subdomain and uses custom routing rules|Implement custom routing rules and SSL termination for multiple apps. Choose this method to remain OpenShift-native; for example, you can use the OpenShift web console to create and manage routes.|<ol><li>[Create a `ClusterIP` service](https://kubernetes.io/docs/concepts/services-networking/service/#defining-a-service){: external} to assign an internal IP address to your app.</li><li>[Create a router that is exposed by a private load balancer.](/docs/openshift?topic=openshift-openshift_routes#private-routes-setup)</li><li>[Set up an OpenShift route](https://docs.openshift.com/container-platform/3.11/dev_guide/routes.html){: external}.</li><li>Customize routing rules with [optional configurations](https://docs.openshift.com/container-platform/3.11/architecture/networking/routes.html){: external}.</li></ol>|
|NodePort|Port on a worker node that exposes the app on the worker's private IP address|Test private access to one app or provide access for only a short amount of time.|<ol><li>[Create a NodePort service](/docs/openshift?topic=openshift-nodeport).</li><li>A NodePort service opens a port on a worker node over both the private and public IP address of the worker node. You must use a [Calico preDNAT network policy](/docs/openshift?topic=openshift-network_policies#block_ingress) to block traffic to the public NodePorts.</li></ol>|
|NLB 1.0|Basic load balancing that exposes the app with a private IP address|Quickly expose one app to a private network with a private IP address.|<ol><li>[Create a private NLB service](/docs/openshift?topic=openshift-loadbalancer).</li><li>An NLB with a portable private IP address still has a public node port open on every worker node. Create a [Calico preDNAT network policy](/docs/openshift?topic=openshift-network_policies#block_ingress) to block traffic to the public NodePorts.</li></ol>|
|NLB v2.0|DSR load balancing that exposes the app with a private IP address|Expose an app that might receive high levels of traffic to a private network with an IP address.|<ol><li>Complete the [prerequisites](/docs/openshift?topic=openshift-loadbalancer-v2#ipvs_provision).</li><li>Create a private NLB 2.0 in a [single-](/docs/openshift?topic=openshift-loadbalancer-v2#ipvs_single_zone_config) or [multizone](/docs/openshift?topic=openshift-loadbalancer-v2#ipvs_multi_zone_config) cluster.</li><li>An NLB with a portable private IP address still has a public node port open on every worker node. Create a [Calico preDNAT network policy](/docs/openshift?topic=openshift-network_policies#block_ingress) to block traffic to the public NodePorts.</li></ol>|
|Ingress ALB|HTTPS load balancing that exposes the app with a subdomain and uses custom routing rules|Implement custom routing rules and SSL termination for multiple apps. Choose this method only if you have specific requirements to use Ingress instead of routes, such as migrating an app that already uses Ingress from a community Kubernetes cluster.|<ol><li>[Disable the public ALB.](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_alb_configure)</li><li>[Enable the private ALB and create an Ingress resource](/docs/openshift?topic=openshift-ingress#ingress_expose_private).</li><li>Customize ALB routing rules with [annotations](/docs/openshift?topic=openshift-ingress_annotation).</li></ol>|
{: caption="Characteristics of network deployment patterns for a public and a private VLAN setup" caption-side="top"}

<br />




