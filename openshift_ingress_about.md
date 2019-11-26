---

copyright:
  years: 2014, 2019
lastupdated: "2019-11-26"

keywords: openshift, roks, rhoks, rhos, nginx, ingress controller

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

# About Ingress ALBs
{: #ingress-about}

Ingress is a Kubernetes service that balances network traffic workloads in your cluster by forwarding public or private requests to your apps. You can use Ingress to expose multiple app services to the public or to a private network by using a unique public or private route.
{: shortdesc}

## What comes with Ingress?
{: #ingress_components}

Ingress consists of three components: Ingress resources, application load balancers (ALBs), and the multizone load balancer (MZLB)<roks311-vpc> for classic clusters or the VPC load balancer for VPC clusters</roks311-vpc>.
{: shortdesc}

### Ingress resource
{: #ingress-resource}

To expose an app by using Ingress, you must create a Kubernetes service for your app and register this service with Ingress by defining an Ingress resource. The Ingress resource is a Kubernetes resource that defines the rules for how to route incoming requests for apps. 
{: shortdesc}

The Ingress resource also specifies the path to your app services. When you create a standard cluster, an Ingress subdomain is registered by default for your cluster in the format `<cluster_name>.<globally_unique_account_HASH>-0001.<region>.containers.appdomain.cloud`. The paths to your app services are appended to the public route to form a unique app URL such as `mycluster-a1b2cdef345678g9hi012j3kl4567890-0001.us-south.containers.appdomain.cloud/myapp1`.

One Ingress resource is required per namespace where you have apps that you want to expose.
* If the apps in your cluster are all in the same namespace, one Ingress resource is required to define routing rules for the apps that are exposed there. Note that if you want to use different domains for the apps within the same namespace, you can use a wildcard domain to specify multiple subdomain hosts within one resource.
* If the apps in your cluster are in different namespaces, you must create one resource per namespace to define rules for the apps that are exposed there. You must use a wildcard domain and specify a different subdomain in each Ingress resource.

For more information, see [Planning networking for single or multiple namespaces](/docs/openshift?topic=openshift-ingress#multiple_namespaces).


<p class="important">As of 22 November 2019, the following changes are made to the Ingress subdomain:</br></br>All new clusters are assigned an Ingress subdomain in the format <code>&lt;cluster_name&gt;.&lt;globally_unique_account_HASH&gt;-0001.&lt;region&gt;.containers.appdomain.cloud</code> and an Ingress secret in the format <code>&lt;cluster_name&gt;.&lt;globally_unique_account_HASH&gt;-0001</code>. For more information about this format, see [Understanding the subdomain format](/docs/openshift?topic=openshift-loadbalancer_hostname#loadbalancer_hostname_format). If you have pipeline dependencies on consistent app domain names, you can use your own custom domain instead of the IBM-provided Ingress subdomain.</br></br>If you have a cluster that is still assigned an Ingress subdomain in the format <code>&lt;cluster_name&gt;.&lt;region&gt;.containers.mybluemix.net</code>, that subdomain is migrated to Cloudflare. An A record that maps to a <code>&lt;cluster_name&gt;.&lt;region_or_zone&gt;.containers.appdomain.cloud</code> subdomain is assigned during migration and is replaced with a CNAME record after migration. The <code>appdomain.cloud</code> subdomain is created and assigned to your cluster for you if it did not exist in your cluster. Either subdomain can still be used.</p>

### Application load balancer (ALB)
{: #alb-about}

The application load balancer (ALB) is an external load balancer that listens for incoming HTTP, HTTPS, or TCP service requests. The ALB then forwards requests to the appropriate app pod according to the rules defined in the Ingress resource.
{: shortdesc}

When you create a standard cluster, Red Hat OpenShift on IBM Cloud automatically creates a highly available ALB in each zone where you have worker nodes and assigns a unique public route which all public ALBs share. You can find the public route for your cluster by running `ibmcloud oc cluster get --cluster <cluster_name_or_ID>` and looking for the **Ingress subdomain** in the format `mycluster-<hash>-0001.us-south.containers.appdomain.cloud`. One default private ALB is also automatically created in each zone of your cluster, but the private ALBs are not automatically enabled and do not use the Ingress subdomain. Note that<roks311-vpc> classic</roks311-vpc> clusters with workers that are connected to private VLANs only are not assigned an IBM-provided Ingress subdomain.<roks311-vpc>

**Classic clusters: ALB IP addresses**</roks311-vpc>

In classic clusters, the Ingress subdomain for your cluster is linked to the public ALB IP addresses. You can find the IP address of each public ALB by running `ibmcloud oc alb ls --cluster <cluster_name_or_ID>` and looking for the **ALB IP** field. The portable public and private ALB IP addresses are provisioned into your IBM Cloud infrastructure account during cluster creation and are static floating IPs that do not change for the life of the cluster. If the worker node is removed, a `Keepalived` daemon that constantly monitors the IP automatically reschedules the ALB pods that were on that worker to another worker node in that zone. The rescheduled ALB pods retain the same static IP address. However, if you remove a zone from a cluster, then the ALB IP address for that zone is removed.<roks311-vpc>

**VPC clusters: ALB hostnames**

When you create a VPC cluster, one public VPC load balancer is automatically created outside of your cluster in your VPC. The public VPC load balancer puts the public IP addresses of your public ALBs behind one hostname. In VPC clusters, a hostname is assigned to the ALBs because the ALB IP addresses are not static and might change over time. You can find the hostname that is assigned to your public ALBs and the hostname that is assigned to your private ALBs by running `ibmcloud oc alb ls --cluster <cluster_name_or_ID>` and looking for the **Load Balancer Hostname** field. Because the private ALBs are disabled by default, a private VPC load balancer that puts four private ALBs behind one hostname is created only when you enable your private ALBs.</roks311-vpc>

### Multizone load balancer (MZLB)<roks311-vpc> or Load Balancer for VPC</roks311-vpc>
{: #mzlb}

<roks311-vpc>Depending on whether you have a classic or VPC cluster, a</roks311-vpc>A Cloudflare multizone load balancer (MZLB)<roks311-vpc> or a Load Balancer for VPC</roks311-vpc> health checks your ALBs.
{: shortdesc}<roks311-vpc>

**Classic clusters: Multizone load balancer (MZLB)**</roks311-vpc>

Whenever you create a multizone cluster or [add a zone to a single zone cluster](/docs/openshift?topic=openshift-add_workers#add_zone), a Cloudflare multizone load balancer (MZLB) is automatically created and deployed so that 1 MZLB exists for each region. The MZLB puts the IP addresses of your ALBs behind the same subdomain and enables health checks on these IP addresses to determine whether they are available or not.

For example, if you have worker nodes in 3 zones in the US-East region, the subdomain `yourcluster.us-east.containers.appdomain.cloud` has 3 ALB IP addresses. The MZLB health checks the public ALB IP in each zone of a region and keeps the DNS lookup results updated based on these health checks. For example, if your ALBs have IP addresses `1.1.1.1`, `2.2.2.2`, and `3.3.3.3`, a normal operation DNS lookup of your Ingress subdomain returns all 3 IPs, 1 of which the client accesses at random. If the ALB with IP address `3.3.3.3` becomes unavailable for any reason, such as due to zone failure, then the health check for that zone fails, the MZLB removes the failed IP from the subdomain, and the DNS lookup returns only the healthy `1.1.1.1` and `2.2.2.2` ALB IPs. The subdomain has a 30 second time to live (TTL), so after 30 seconds, new client apps can access only one of the available, healthy ALB IPs.

In rare cases, some DNS resolvers or client apps might continue to use the unhealthy ALB IP after the 30-second TTL. These client apps might experience a longer load time until the client app abandons the `3.3.3.3` IP and tries to connect to `1.1.1.1` or `2.2.2.2`. Depending on the client browser or client app settings, the delay can range from a few seconds to a full TCP timeout.

The MZLB load balances for public ALBs that use the IBM-provided Ingress subdomain only. If you use only private ALBs, you must manually check the health of the ALBs and update DNS lookup results. If you use public ALBs that use a custom domain, you can include the ALBs in MZLB load balancing by creating a CNAME in your DNS entry to forward requests from your custom domain to the IBM-provided Ingress subdomain for your cluster.

If you use Calico pre-DNAT network policies to block all incoming traffic to Ingress services, you must also whitelist [Cloudflare's IPv4 IPs ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.cloudflare.com/ips/) that are used to check the health of your ALBs. For steps on how to create a Calico pre-DNAT policy to whitelist these IPs, see [Lesson 3 of the Calico network policy tutorial](/docs/containers?topic=containers-policy_tutorial#lesson3).
{: note}<roks311-vpc>

**VPC clusters: Load Balancer for VPC**

When you create a VPC cluster, one public and one private VPC load balancer is automatically created outside of your cluster in your VPC. The public VPC load balancer puts the public IP addresses of your public ALBs behind one hostname, and the private VPC load balancer puts the private IP addresses of your private ALBs behind one hostname. In VPC clusters, a hostname is assigned to the ALBs because the ALB IP addresses are not static and might change over time.

The Ingress subdomain for your cluster is automatically linked to the VPC load balancer hostname for your public ALBs. Note that the Ingress subdomain for your cluster is different than the VPC load balancer-assigned hostname for your public ALBs. The Ingress subdomain is the public route through which users access your app from the internet, and can be configured to use TLS termination. The assigned hostname for your public ALBs is what the VPC load balancer uses to forward the user requests to your ALBs. You can also use the hostname for your public ALBs to access your apps, but the hostname cannot be configured to use TLS termination.

Before forwarding traffic to ALBs, the VPC load balancer also health checks the public ALB IP addresses that are behind the hostname to determine whether the ALBs are available or not. Every 5 seconds, the VPC load balancer health checks the floating public ALB IPs for your cluster and keeps the DNS lookup results updated based on these health checks. When a user sends a request to your app by using the cluster's Ingress subdomain and app route, such as `mycluster-<hash>-0001.us-south.containers.appdomain.cloud/myapp`, the VPC load balancer receives the request. If all ALBs are healthy, a normal operation DNS lookup of your Ingress subdomain returns all of the floating IPs, 1 of which the client accesses at random. However, if one IP becomes unavailable for any reason, then the health check for that IP fails after 2 retries. The VPC load balancer removes the failed IP from the subdomain, and the DNS lookup returns only the healthy IPs while a new floating IP address is generated.

Note that the VPC load balancer health checks only public ALBs and updates DNS lookup results for the Ingress subdomain. If you use only private ALBs, you must manually health check them and update DNS lookup results.</roks311-vpc>

<br />


## How does a request get to my app with Ingress<roks311-vpc> in a classic cluster</roks311-vpc>?
{: #architecture-classic}

### Single-zone cluster
{: #classic-single}

The following diagram shows how Ingress directs communication from the internet to an app in a classic single-zone cluster.
{: shortdesc}

<img src="images/cs_ingress_singlezone.png" width="600" alt="Expose an app in a single-zone cluster by using Ingress" style="width:600px; border-style: none"/>

1. A user sends a request to your app by accessing your app's URL. This URL is the Ingress subdomain for your cluster appended with the Ingress resource path for your exposed app, such as `mycluster-<hash>-0001.us-south.containers.appdomain.cloud/myapp`.

2. A DNS system service resolves the subdomain in the URL to the portable public IP address of the load balancer that exposes the ALB in your cluster.

3. Based on the resolved IP address, the client sends the request to the Kubernetes load balancer service that exposes the ALB.

4. The load balancer service routes the request to the ALB.

5. The ALB checks if a routing rule for the `myapp` path in the cluster exists. If a matching rule is found, the request is proxied according to the rules that you defined in the Ingress resource to the pod where the app is deployed. The source IP address of the package is changed to the IP address of the public IP address of the worker node where the app pod runs. If multiple app instances are deployed in the cluster, the ALB load balances the requests between the app pods.

6. When the app returns a response packet, it uses the IP address of the worker node where the ALB that forwarded the client request exists. The ALB then sends the response packet to the client.

### Multizone cluster
{: #classic-multi}

The following diagram shows how Ingress directs communication from the internet to an app in a classic multizone cluster.
{: shortdesc}

<img src="images/cs_ingress_multizone.png" width="800" alt="Expose an app in a multizone cluster by using Ingress" style="width:800px; border-style: none"/>

1. A user sends a request to your app by accessing your app's URL. This URL is the Ingress subdomain for your cluster appended with the Ingress resource path for your exposed app, such as `mycluster-<hash>-0001.us-south.containers.appdomain.cloud/myapp`.

2. A DNS system service, which acts as the global load balancer, resolves the subdomain in the URL to an available IP address that was reported as healthy by the MZLB. The MZLB continuously checks the portable public IP addresses of the load balancer services that expose public ALBs in each zone in your cluster. The IP addresses are resolved in a round-robin cycle, ensuring that requests are equally load balanced among the healthy ALBs in various zones.

3. The client sends the request to the IP address of the Kubernetes load balancer service that exposes an ALB.

4. The load balancer service routes the request to the ALB.

5. The ALB checks if a routing rule for the `myapp` path in the cluster exists. If a matching rule is found, the request is proxied according to the rules that you defined in the Ingress resource to the pod where the app is deployed. The source IP address of the package is changed to the public IP address of the worker node where the app pod runs. If multiple app instances are deployed in the cluster, the ALB load balances the requests between app pods across all zones.

6. When the app returns a response packet, it uses the IP address of the worker node where the ALB that forwarded the client request exists. The ALB then sends the response packet to the client.<roks311-vpc>

## How does a request get to my app with Ingress in a VPC cluster?
{: #architecture-vpc}

The following diagram shows how Ingress directs communication from the internet to an app in a VPC multizone cluster.
{: shortdesc}

image <img src="images/cs_ingress_vpc.png" width="830" alt="Expose an app in a VPC cluster by using Ingress" style="width:830px; border-style: none"/>

1. A user sends a request to your app by accessing your app's URL. This URL is the public URL for your exposed app appended with the Ingress resource path, such as `mycluster-<hash>-0001.us-south.containers.appdomain.cloud/myapp`.

2. A DNS system service resolves the subdomain in the URL to an available ALB IP address that was reported as healthy by the VPC load balancer. The VPC load balancer continuously checks the floating ALB IP addresses that are behind the ALBs' assigned hostname.

3. Based on the resolved IP address, the client sends the request to the VPC load balancer that exposes your cluster's ALBs.

4. The VPC load balancer service routes the request to an ALB. Each ALB routes requests to the app instances in its own zone and to app instances in other zones. Additionally, if multiple app instances are deployed in one zone, the ALB routes the requests between the app pods in the zone.

5. The ALB checks if a routing rule for the `myapp` path in the cluster exists. If a matching rule is found, the request is proxied according to the rules that you defined in the Ingress resource to the pod where the app is deployed. The source IP address of the package is changed to the public IP address of the worker node where the app pod runs. If multiple app instances are deployed in the cluster, the ALB load balances the requests between app pods across all zones.</roks311-vpc>



