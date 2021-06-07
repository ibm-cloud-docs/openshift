---

copyright:
  years: 2014, 2021
lastupdated: "2021-06-07"

keywords: openshift, roks, rhoks, rhos, networking

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
  


# Choosing an app exposure service
{: #cs_network_planning}

Securely expose your apps to external traffic by using {{site.data.keyword.openshiftshort}} routes or {{site.data.keyword.containerlong}} NodePort, network load balancer, or Ingress application load balancer services.
{: shortdesc}

## Understanding options for exposing apps
{: #external}

To securely expose your apps to external traffic, you can use choose from the following services.
{: shortdesc}

<dl>
<dt>[{{site.data.keyword.openshiftshort}} route](/docs/openshift?topic=openshift-openshift_routes)</dt>
<dd>A route exposes a service as a hostname in the format `<service_name>-<project>.<cluster_name>-<random_hash>-0001.<region>.containers.appdomain.cloud`. A router is deployed by default to your cluster, which enable routes to be used by external clients. The router uses the service selector to find the service and the endpoints that back the service. You can configure the service selector to direct traffic through one route to multiple services. You can also create either unsecured or secured routes by using the TLS certificate that is assigned by the router for your hostname. Note that the router supports only the HTTP and HTTPS protocols.</dd>

<dt>[NodePort](/docs/openshift?topic=openshift-nodeport)</dt>
<dd>When you expose apps with a NodePort service, a NodePort in the range of 30000 - 32767 and an internal cluster IP address is assigned to the service. To access the service from outside the cluster, you use the public or private IP address of any worker node and the NodePort in the format <code>&lt;IP_address&gt;:&lt;nodeport&gt;</code>. However, the public and private IP addresses of the worker node are not permanent. When a worker node is removed or re-created, a new public and a new private IP address are assigned to the worker node. NodePorts are ideal for testing public or private access or providing access for only a short amount of time.</dd>

<dt>LoadBalancer</dt>
<dd>The LoadBalancer service type is implemented differently depending on your cluster's infrastructure provider.<ul>
<li><img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> **Classic clusters**: [Network load balancer (NLB)](/docs/openshift?topic=openshift-loadbalancer). Every standard cluster is provisioned with four portable public and four portable private IP addresses that you can use to create a layer 4 TCP/UDP network load balancer (NLB) for your app. You can customize your NLB by exposing any port that your app requires. The portable public and private IP addresses that are assigned to the NLB are permanent and do not change when a worker node is re-created in the cluster. If you create public NLBs, you can create a subdomain for your app that registers the public NLB IP addresses with a DNS entry. You can also enable health check monitors on the NLB IPs for each subdomain.</li>
<li><img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> **VPC clusters**: [Load Balancer for VPC](/docs/openshift?topic=openshift-vpc-lbaas). When you create a Kubernetes LoadBalancer service for an app in your cluster, a layer 7 VPC load balancer is automatically created in your VPC outside of your cluster. The VPC load balancer is multizonal and routes requests for your app through the private NodePorts that are automatically opened on your worker nodes. By default, the load balancer is also created with a hostname that you can use to access your app, but you can also create a subdomain for your app that creates a DNS entry.</li>
</ul></dd>

<dt>Ingress</dt>
<dd><img src="images/icon-version-43.png" alt="Version 4 icon" width="30" style="width:30px; border-style: none"/> **{{site.data.keyword.openshiftshort}} version 4 clusters**: Expose multiple apps in a cluster by setting up routing with the [{{site.data.keyword.openshiftshort}} Ingress controller](/docs/openshift?topic=openshift-ingress-roks4). The Ingress controller uses the Ingress subdomain as a secured and unique public or private entry point to route incoming requests. You can use one subdomain to expose multiple apps in your cluster as services. Ingress consists of three components:<ul>
  <li>The Ingress controller is a HAProxy-based Kubernetes service that manages all incoming traffic for the apps in your cluster by implementing routing rules for the apps. This controller is managed by the Ingress operator.</li>
  <li>The router listens for incoming HTTP, HTTPS, or TCP service requests, and then forwards requests to the pods for that app only according to the rules defined in the Ingress resource and implemented by the Ingress controller.</li>
  <li>The Ingress resource defines the rules for how to route and load balance incoming requests for an app.</li></ul></dd>
</dl>

## Choosing among load balancing solutions
{: #routes-vs-ingress}

Now that you understand what [options](#external) you have to expose apps in your {{site.data.keyword.openshiftshort}} cluster, choose the best solution for your workload.
{: shortdesc}

**Do I use {{site.data.keyword.openshiftshort}} routes or Ingress?**

Because routes and Ingress offer similar capabilities, both load balancing solutions might be suitable to your workload. To help decide between routes and Ingress, consider the following broader concerns.
* **Portability across clouds**: If you anticipate running the same app in {{site.data.keyword.openshiftshort}} clusters in a hybrid scenario across multiple cloud providers, use the {{site.data.keyword.openshiftshort}} router. Routes are configured and work the same way across cloud providers, whereas Ingress might vary with each provider.
* **Annotations to extend routing capabilities**: With the Ingress ALB, you can customize Ingress routing rules with annotations. Some of these annotations help to integrate other {{site.data.keyword.cloud_notm}} services to your routes, such as {{site.data.keyword.appid_short}} to provide authentication for the Ingress URL that is assigned to your app. These annotations are not available for the {{site.data.keyword.openshiftshort}} router, which must use [route-specific `haproxy` annotations](https://docs.openshift.com/container-platform/4.6/networking/routes/route-configuration.html#nw-route-specific-annotations_route-configuration){: external}.

The following table compares the features of each app exposure method.

|Characteristics|NodePort|LoadBalancer (Classic - NLB)|LoadBalancer (VPC load balancer)|Ingress controller|Route|
|---------------|------|--------|---|-----------|
|Stable external IP| |<img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" />| |<img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" />|<img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" />|
|External hostname| |<img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" />|<img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" />|<img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" />|<img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" />|
|SSL termination| |<img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" />*|<img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" />*|<img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" />|<img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" />|
|HTTP(S) load balancing| | | |<img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" />|<img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" />|
|Custom routing rules| | | |<img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" />|<img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" />|
|Multiple apps per route or service| | | |<img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" />|<img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" />|
|{{site.data.keyword.cloud_notm}} extensions like {{site.data.keyword.appid_short}}| | | |<img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" />| |
|Consistent hybrid multicloud deployment| | | | |<img src="images/confirm.svg" width="32" alt="Feature available" style="width:32px;" />|
{: class="simple-tab-table"}
{: caption="Comparison of external networking for apps in {{site.data.keyword.openshiftshort}} version 4 clusters." caption-side="top"}
{: #roks-net-compare-43}
{: tab-title="{{site.data.keyword.openshiftshort}} 4"}
{: tab-group="openshift-network-compare"}

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
{: class="simple-tab-table"}
{: caption="Comparison of external networking for apps in {{site.data.keyword.openshiftshort}} version 3.11 clusters." caption-side="top"}
{: #roks-net-compare-311}
{: tab-title="{{site.data.keyword.openshiftshort}} 3.11"}
{: tab-group="openshift-network-compare"}

`*` SSL termination is provided by `ibmcloud oc nlb-dns` commands. In classic clusters, these commands are supported for public NLBs only.
{: note}

<br />

## Planning public external load balancing
{: #openshift_routers}

Publicly expose an app in your cluster to the internet.
{: shortdesc}

In <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> **classic** clusters, your worker nodes are connected to a public VLAN. The public VLAN determines the public IP address that is assigned to each worker node, which provides each worker node with a public network interface. Public networking services connect to this public network interface by providing your app with a public IP address and, optionally, a public URL.

In <img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> **VPC** clusters, your worker nodes are connected to private VPC subnets only. However, when you create public networking services, a VPC load balancer is automatically created. The VPC load balancer can route public requests to your app by providing your app a public URL. When an app is publicly exposed, anyone that has the public URL can send a request to your app.

When an app is publicly exposed, anyone that has the public service IP address or the URL that you set up for your app can send a request to your app. For this reason, expose as few apps as possible. Expose an app to the public only when your app is ready to accept traffic from external web clients or users.

The public network interface for worker nodes is protected by [predefined Calico network policy settings](/docs/openshift?topic=openshift-network_policies#default_policy) that are configured on every worker node during cluster creation. By default, all outbound network traffic is allowed for all worker nodes. Inbound network traffic is blocked except for a few ports. These ports are opened so that IBM can monitor network traffic and automatically install security updates for the Kubernetes master, and so that connections can be established to public networking services. For more information about these policies, including how to modify them, see [Network policies](/docs/openshift?topic=openshift-network_policies#network_policies).

### Public app networking for classic clusters
{: #pattern_public}

<img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> To make an app publicly available to the internet in a classic cluster, choose an app exposure method that uses routes, NodePorts, NLBs, or setting up Ingress. The following table describes each possible method, why you might use it, and how to set it up. For basic information about the networking services that are listed, see [Understanding Kubernetes service types](#external).
{: shortdesc}

You cannot use multiple app exposure methods for one app.
{: note}

<table summary="This table reads left to right about the name, characteristics, use cases, and deployment steps of public network deployment patterns.">
<caption>Characteristics of public app exposure methods in {{site.data.keyword.openshiftlong_notm}}</caption>
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
<td>Implement custom routing rules and SSL termination for multiple apps. Choose this method to remain {{site.data.keyword.openshiftshort}}-native; for example, you can use the {{site.data.keyword.openshiftshort}} web console to create and manage routes.</td>
<td><ol><li>[Create a `ClusterIP` service ![External link icon](../icons/launch-glyph.svg "External link icon")](https://kubernetes.io/docs/concepts/services-networking/service/#defining-a-service) to assign an internal IP address to your app.</li><li>[Set up an {{site.data.keyword.openshiftshort}} route ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/4.6/applications/deployments/route-based-deployment-strategies.html).</li><li>Customize routing rules with [optional configurations ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/4.6/networking/routes/route-configuration.html).</li></ol></td>
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
<td>{{site.data.keyword.openshiftshort}} version 4 clusters: Ingress controller</td>
<td>HTTP(S) load balancing that exposes the app with a subdomain and uses custom routing rules</td>
<td>Implement custom routing rules and SSL termination for multiple apps.</td>
<td>Create an [Ingress resource](/docs/openshift?topic=openshift-ingress-roks4#ingress-roks4-public) for the default public Ingress controller.</td>
</tr>
</tbody>
</table>

### Public app networking for VPC clusters
{: #pattern_public_vpc}

<img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> To make an app publicly available to the internet in a VPC cluster, choose an app exposure method that uses routes, VPC load balancers, or setting up Ingress. The following table describes each possible method, why you might use it, and how to set it up. For basic information about the networking services that are listed, see [Understanding Kubernetes service types](#external).
{: shortdesc}

You cannot use multiple app exposure methods for one app.
{: note}

<table summary="This table reads left to right about the name, characteristics, use cases, and deployment steps of public network deployment patterns.">
<caption>Characteristics of public app exposure methods in {{site.data.keyword.openshiftlong_notm}}</caption>
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
<td>Implement custom routing rules and SSL termination for multiple apps. Choose this method to remain {{site.data.keyword.openshiftshort}}-native; for example, you can use the {{site.data.keyword.openshiftshort}} web console to create and manage routes.</td>
<td>[Create a route by using the default public router in clusters with a public cloud service endpoint](/docs/openshift?topic=openshift-openshift_routes#routes-public-classic), or [create a route by using a custom public router in clusters with a private cloud service endpoint only](/docs/openshift?topic=openshift-openshift_routes#routes-public-vpc-privse).</td>
</tr>
<tr>
<td>VPC load balancer</td>
<td>Basic load balancing that exposes the app with a hostname</td>
<td>Quickly expose one app to the public with a VPC load balancer-assigned hostname.</td>
<td>[Create a public `LoadBalancer` service](/docs/openshift?topic=openshift-vpc-lbaas) in your cluster. A multizonal VPC load balancer is automatically created in your VPC that assigns a hostname to your `LoadBalancer` service for your app.</td>
</tr>
<tr>
<td>{{site.data.keyword.openshiftshort}} version 4 clusters: Ingress controller</td>
<td>HTTP(S) load balancing that exposes the app with a subdomain and uses custom routing rules</td>
<td>Implement custom routing rules and SSL termination for multiple apps.</td>
<td>[Create an Ingress resource for the default public Ingress controller in clusters with a public cloud service endpoint](/docs/openshift?topic=openshift-ingress-roks4#ingress-roks4-public), or [create an Ingress resource for a custom public Ingress controller in clusters with a private cloud service endpoint only](/docs/openshift?topic=openshift-ingress-roks4#priv-se-pub-controller).</td>
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
* In classic clusters, if you have [VRF or VLAN spanning](/docs/openshift?topic=openshift-subnets#basics_segmentation) enabled, any system that is connected to any of the private VLANs in the same {{site.data.keyword.cloud_notm}} account.
* In VPC clusters:
  * If traffic is permitted between VPC subnets, any system in the same VPC.
  * If traffic is permitted between VPCs, any system that has access to the VPC that the cluster is in.

### Private app networking for classic clusters
{: #private_both_vlans}

<img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> When your worker nodes are connected to both a public and a private VLAN, you can make your app accessible from a private network only by creating private routes, NodePorts, NLBs, or setting up Ingress. Then, you can create Calico policies to block public traffic to the services.
{: shortdesc}

The public network interface for worker nodes is protected by [predefined Calico network policy settings](/docs/openshift?topic=openshift-network_policies#default_policy) that are configured on every worker node during cluster creation. By default, all outbound network traffic is allowed for all worker nodes. Inbound network traffic is blocked except for a few ports. These ports are opened so that IBM can monitor network traffic and automatically install security updates for the Kubernetes master, and so that connections can be established to NodePort, LoadBalancer, and Ingress services.

Because the default Calico network policies allow inbound public traffic to these services, you can create Calico policies to instead block all public traffic to the services. For example, a NodePort service opens a port on a worker node over both the private and public IP address of the worker node. An NLB service with a portable private IP address opens a public NodePort on every worker node. You must create a [Calico preDNAT network policy](/docs/openshift?topic=openshift-network_policies#block_ingress) to block public NodePorts.

Check out the following methods for private app networking:

|Name|Load-balancing method|Use case|Implementation|
|----|---------------------|--------|--------------|
|Route|HTTP(S) load balancing that exposes the app with a subdomain and uses custom routing rules|Implement custom routing rules and SSL termination for multiple apps. Choose this method to remain {{site.data.keyword.openshiftshort}}-native; for example, you can use the {{site.data.keyword.openshiftshort}} web console to create and manage routes.|<ol><li>[Create a `ClusterIP` service](https://kubernetes.io/docs/concepts/services-networking/service/#defining-a-service){: external} to assign an internal IP address to your app.</li><li>[Create a router that is exposed by a private load balancer.](/docs/openshift?topic=openshift-openshift_routes#private-routes-setup-43)</li><li>[Set up an {{site.data.keyword.openshiftshort}} route](https://docs.openshift.com/container-platform/4.6/applications/deployments/route-based-deployment-strategies.html){: external}.</li><li>Customize routing rules with [optional configurations](https://docs.openshift.com/container-platform/4.6/networking/routes/route-configuration.html){: external}.</li></ol>|
|NodePort|Port on a worker node that exposes the app on the worker's private IP address|Test private access to one app or provide access for only a short amount of time.|<ol><li>[Create a NodePort service](/docs/openshift?topic=openshift-nodeport).</li><li>A NodePort service opens a port on a worker node over both the private and public IP address of the worker node. You must use a [Calico preDNAT network policy](/docs/openshift?topic=openshift-network_policies#block_ingress) to block traffic to the public NodePorts.</li></ol>|
|NLB 1.0|Basic load balancing that exposes the app with a private IP address|Quickly expose one app to a private network with a private IP address.|<ol><li>[Create a private NLB service](/docs/openshift?topic=openshift-loadbalancer).</li><li>An NLB with a portable private IP address still has a public node port open on every worker node. Create a [Calico preDNAT network policy](/docs/openshift?topic=openshift-network_policies#block_ingress) to block traffic to the public NodePorts.</li></ol>|
|NLB v2.0|DSR load balancing that exposes the app with a private IP address|Expose an app that might receive high levels of traffic to a private network with an IP address.|<ol><li>Complete the [prerequisites](/docs/openshift?topic=openshift-loadbalancer-v2#ipvs_provision).</li><li>Create a private NLB 2.0 in a [single-](/docs/openshift?topic=openshift-loadbalancer-v2#ipvs_single_zone_config) or [multizone](/docs/openshift?topic=openshift-loadbalancer-v2#ipvs_multi_zone_config) cluster.</li><li>An NLB with a portable private IP address still has a public node port open on every worker node. Create a [Calico preDNAT network policy](/docs/openshift?topic=openshift-network_policies#block_ingress) to block traffic to the public NodePorts.</li></ol>|
|{{site.data.keyword.openshiftshort}} version 4 clusters: Ingress controller|HTTP(S) load balancing that exposes the app with a subdomain and uses custom routing rules|Implement custom routing rules and SSL termination for multiple apps.|<ol><li>[Register your custom domain](/docs/openshift?topic=openshift-ingress-roks4#ingress-roks4-private-2).</li><li>[Create and configure a private Ingress controller](/docs/openshift?topic=openshift-ingress-roks4#ingress-roks4-private-3).</li><li>Create an [Ingress resource](/docs/openshift?topic=openshift-ingress-roks4#ingress-roks4-private-4) for the private Ingress controller.</li></ol>|
{: caption="Characteristics of network deployment patterns for a public and a private VLAN setup" caption-side="top"}

<br />



### Private app networking for VPC clusters
{: #private_vpc}

<img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> To make an app available over a private network only in a VPC cluster, choose a load balancing deployment pattern based on your cluster's service endpoint setup: public and private cloud service endpoint, or private cloud service endpoint only. For each service endpoint setup, the following table describes each possible app exposure method, why you might use it, and how to set it up.
{: shortdesc}

<p class="note"> <img src="images/icon-version-43.png" alt="Version 4 icon" width="30" style="width:30px; border-style: none"/> Only version 4 clusters can be created on VPC infrastructure. The following methods do not apply to version 3.11 clusters, which can be created on classic infrastructure only.</br></br>You cannot use multiple app exposure methods for one app.</p>

|Name|Load-balancing method|Use case|Implementation|
|----|---------------------|--------|--------------|
|Route|HTTP(S) load balancing that exposes the app with a subdomain and uses custom routing rules|Implement custom routing rules and SSL termination for multiple apps. Choose this method to remain {{site.data.keyword.openshiftshort}}-native; for example, you can use the {{site.data.keyword.openshiftshort}} web console to create and manage routes.|[Create a route by using the default private router in clusters with a private cloud service endpoint only](/docs/openshift?topic=openshift-openshift_routes#private-routes-setup-43), or [create a route by using a custom private router in clusters with a public cloud service endpoint](/docs/openshift?topic=openshift-openshift_routes#routes-private-vpc-privse).|
|NodePort|Port on a worker node that exposes the app on the worker's private IP address|Test private access to one app or provide access for only a short amount of time.|[Create a private NodePort service](/docs/openshift?topic=openshift-nodeport).|
|VPC load balancer|Basic load balancing that exposes the app with a private hostname|Quickly expose one app to a private network with a VPC load balancer-assigned private hostname.|[Create a private `LoadBalancer` service](/docs/openshift?topic=openshift-vpc-lbaas) in your cluster. A multizonal VPC load balancer is automatically created in your VPC that assigns a hostname to your `LoadBalancer` service for your app.|
|Ingress controller|HTTP(S) load balancing that exposes the app with a subdomain and uses custom routing rules|Implement custom routing rules and SSL termination for multiple apps.|[Create an Ingress resource for the default private Ingress controller in clusters with a private cloud service endpoint only](/docs/openshift?topic=openshift-ingress-roks4#priv-se-priv-controller), or [create an Ingress resource for a custom private Ingress controller in clusters with a public cloud service endpoint](/docs/openshift?topic=openshift-ingress-roks4#ingress-roks4-private).|
{: caption="Private network deployment patterns for a VPC cluster" caption-side="top"}
