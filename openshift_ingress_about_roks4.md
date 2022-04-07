---

copyright:
  years: 2014, 2022
lastupdated: "2022-04-07"

keywords: openshift, nginx, ingress controller, ingress operator, router

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}


# About Ingress
{: #ingress-about-roks4}

![Version 4 icon.](images/icon-version-43.png) This information is for clusters that run {{site.data.keyword.redhat_openshift_notm}} version 4 only.
{: note}

Ingress is a service that balances network traffic workloads in your cluster by forwarding public or private requests to your apps. You can use Ingress to expose multiple app services to the public or to a private network by using a unique public or private domain.
{: shortdesc}

In your cluster, the {{site.data.keyword.redhat_openshift_notm}} Ingress controller is a layer 7 load balancer which implements an HAProxy Ingress controller. A layer 4 `LoadBalancer` service exposes the Ingress controller so that the Ingress controller can receive external requests that come into your cluster. The Ingress controller then forwards requests to app pods in your cluster based on distinguishing layer 7 protocol characteristics, such as headers.

## What are the components of Ingress?
{: #ingress_roks4_components}

In clusters that run {{site.data.keyword.redhat_openshift_notm}} version 4, Ingress consists of three components: an Ingress operator, an Ingress controller, and Route resources. 
{: shortdesc}

### Ingress operator
{: #ingress-operator}

The [{{site.data.keyword.redhat_openshift_notm}} Ingress operator](https://docs.openshift.com/container-platform/4.9/networking/ingress-operator.html){: external} implements routing rules that are applied to all incoming traffic for the apps in your cluster.
{: shortdesc}

Ingress controllers are managed by the Ingress operator. During cluster creation, the default Ingress controller is registered with the default Ingress subdomain for your cluster in the format `<cluster_name>.<globally_unique_account_HASH>-0000.<region>.containers.appdomain.cloud`. When you register your app with this subdomain by creating an Route resource, the Ingress controller ensures that requests to your app through this subdomain are properly proxied to your app pods. To see the default Ingress controller in your cluster, run `oc describe ingresscontroller/default -n openshift-ingress-operator`.

If you want to register your app with a different domain, you can [create a custom Ingress controller](/docs/openshift?topic=openshift-ingress-roks4#ingress-roks4-public-2) that implements routing rules for a custom domain instead.

### Ingress controller
{: #ingress-controller}

One HAProxy-based {{site.data.keyword.redhat_openshift_notm}} Ingress controller is created for each IngressController, and one Ingress controller service is created in each zone where you have worker nodes.
{: shortdesc}

The Ingress operator configures the Ingress controller with the same domain that is specified in the IngressController. The Ingress controller listens for incoming HTTP, HTTPS, or TCP service requests through that domain. The Ingress controller's load balancer service component then forwards requests to the pods for that app only according to the rules defined in the Route resource and implemented by the Ingress controller.

If you have a multizone cluster, one high-availability Ingress controller is deployed to your cluster and is configured with a multizone VPC load balancer. Two worker nodes are required per zone so that the two replicas of the Ingress controller can be deployed and updated correctly.

If you manually create an Ingress controller, the Ingress controller is not automatically registered with the Ingress subdomain or an app in your cluster.
{: note}

![Classic infrastructure provider icon.](images/icon-classic-2.svg) **Classic clusters: Ingress controller IP addresses**

To find the IP addresses of the default Ingress controller services, run `oc get svc -n openshift-ingress` and look for the **EXTERNAL IP** field. If you have a multizone cluster, note that the Ingress controller service in the first zone where you have workers nodes is always named `router-default`, and Ingress controller services in the zones that you subsequently add to your cluster have names such as `router-dal12`.

![VPC infrastructure provider icon.](images/icon-vpc-2.svg) **VPC clusters: Ingress controller hostnames**

When you create a VPC cluster, one public and one private multizone VPC load balancer are automatically created outside of your cluster in your VPC. The public VPC load balancer creates a hostname to register the public Ingress controller, and the private VPC load balancer creates a hostname to register the private Ingress controller. In VPC clusters, a hostname is assigned to the Ingress controllers because external IP addresses are not static and might change over time. Note that this Ingress controller hostname is different than the default Ingress subdomain for your cluster.

The Ingress subdomain for your cluster is automatically linked to the VPC load balancer hostname for your public Ingress controller. Note that the Ingress subdomain for your cluster, which looks like `<cluster_name>.<hash>-0000.<region>.containers.appdomain.cloud`, is different than the VPC load balancer-assigned hostname for your public Ingress controller, which looks like `01ab23cd-<region>.lb.appdomain.cloud`. The Ingress subdomain is the public route through which users access your app from the internet, and can be configured to use TLS termination. The assigned hostname for your public Ingress controller is what the VPC load balancer uses to forward traffic to the Ingress controller service.

You can find the hostname that is assigned to your public Ingress controller and the hostname that is assigned to your private Ingress controller by running `oc get svc -n openshift-ingress` and looking for the **EXTERNAL IP** field.

In your VPC infrastructure dashboard, the VPC load balancer reports as healthy only the two worker nodes that run the Ingress controller replica pods, because these worker nodes are configured as the listeners for the VPC load balancer. Even though only the listener worker nodes are reported as healthy, the listeners' backend pool of worker nodes is kept up-to-date by {{site.data.keyword.openshiftlong_notm}} so that all worker nodes in your cluster can still receive requests from the VPC load balancer.
{: note}

### Route resource
{: #route-resource-about}

To expose an app by using Route, you must create a Kubernetes service for your app and register this service with the Ingress controller by defining an Route resource. The Ingress resource is a {{site.data.keyword.redhat_openshift_notm}} resource that defines the rules for how to route incoming requests for apps.
{: shortdesc}

The Route resource also specifies the path to your app services. The paths to your app services are appended to your cluster's Ingress subdomain to form a unique app URL such as `mycluster-a1b2cdef345678g9hi012j3kl4567890-0000.us-south.containers.appdomain.cloud/myapp1`.

One Route resource is required for each project where you have apps that you want to expose.
* If the apps in your cluster are all in the same project, you must create one Route resource to define the routing rules for the apps that you want to expose. Note that if you want to use different domains for the apps within the same project, you can create one resource per domain.
* If the apps in your cluster are in different projects, you must create one Route resource for each project to define the app's routing rules.

For more information, see [Planning networking for single or multiple projects](/docs/openshift?topic=openshift-ingress-roks4#multiple_projects).

If you want to customize routing rules for your app, you can use [route-specific HAProxy annotations](/docs/openshift?topic=openshift-ingress-roks4#annotations-roks4) that manages traffic for your app. These supported annotations are in the format `haproxy.router.openshift.io/<annotation>`  or `router.openshift.io/<annotation>`. Note that {{site.data.keyword.containerlong_notm}} annotations (`ingress.bluemix.net/<annotation>`) and NGINX annotations (`nginx.ingress.kubernetes.io/<annotation>`) are not supported for the Ingress controller or the Route resource in {{site.data.keyword.redhat_openshift_notm}} version 4.
{: important}



## How does a request get to my app in a classic cluster?
{: #roks4-flow}

### Single-zone cluster
{: #classic-single-roks4}

![Classic infrastructure provider icon.](images/icon-classic-2.svg) The following diagram shows how Ingress directs communication from the internet to an app in a classic single-zone cluster.
{: shortdesc}

![Expose an app in a single-zone cluster by using Ingress](/images/roks_router_ingress_single.png "Expose an app in a single-zone cluster by using Ingress"){: caption="Figure 1. Expose an app in a single-zone cluster by using Ingress" caption-side="bottom"}

1. A user sends a request to your app by accessing your app's URL. This URL is the Ingress subdomain for your cluster appended with the Ingress resource path for your exposed app, such as `mycluster-<hash>-0000.us-south.containers.appdomain.cloud/myapp`.

2. A DNS system service resolves the subdomain in the URL to the portable public IP address of the load balancer that exposes the Ingress controller in your cluster.

3. Based on the resolved IP address, the client sends the request to the Ingress controller service.

4. The Ingress controller checks the routing rules that are implemented by the Ingress controller for a routing rule for the `myapp` path. If a matching rule is found, the request is proxied according to the rules that you defined in the Ingress controller and the Route resource to the pod where the app is deployed. The source IP address of the packet is changed to the IP address of the worker node where the Ingress controller pod runs. If multiple app instances are deployed in the cluster, the Ingress controller load balances the requests between the app pods.

5. When the app returns a response packet, it uses the IP address of the worker node where the Ingress controller that forwarded the request exists. The Ingress controller then sends the response packet to the client.

### Multizone cluster
{: #classic-multi-roks4}

![Classic infrastructure provider icon.](images/icon-classic-2.svg) The following diagram shows how Ingress directs communication from the internet to an app in a classic multizone cluster.
{: shortdesc}

![Expose an app in a multizone cluster by using Ingress](/images/roks_router_ingress_multizone.png "Expose an app in a multizone cluster by using Ingress"){: caption="Figure 1. Expose an app in a multizone cluster by using Ingress" caption-side="bottom"}

1. A user sends a request to your app by accessing your app's URL. This URL is the Ingress subdomain for your cluster appended with the Ingress resource path for your exposed app, such as `mycluster-<hash>-0000.us-south.containers.appdomain.cloud/myapp`.

2. A DNS system service resolves the route subdomain to the floating public IP address of an Ingress controller service that was reported as healthy by the MZLB. The MZLB continuously checks the portable public IP addresses of the services that expose the Ingress controller in each zone in your cluster. Requests are handled by the Ingress controller services in various zones in a round-robin cycle.

3. The client sends the request to the IP address of the service that exposes the Ingress controller.

4. The Ingress controller checks the routing rules that are implemented by the Ingress controller for the `myapp` path. If a matching rule is found, the request is proxied according to the rules that you defined in the IngressController and the Route resource to the pod where the app is deployed. The source IP address of the packet is changed to the IP address of the worker node where the Ingress controller pod runs. If multiple app instances are deployed in the cluster, the Ingress controller service sends the requests between the app pods across all zones.

5. When the app returns a response packet, it uses the IP address of the worker node where the Ingress controller service that forwarded the request exists. The Ingress controller then sends the response packet to the client.

## How does a request get to my app in a VPC cluster?
{: #architecture-vpc}

### VPC cluster with a public cloud service endpoint
{: #architecture-vpc_public}

![VPC infrastructure provider icon.](images/icon-vpc-2.svg) When you create a multizone VPC cluster with the public cloud service endpoint enabled, a public Ingress controller is created by default. The following diagram shows how Ingress directs communication from the internet to an app in a VPC multizone cluster.
{: shortdesc}

![Publicly expose an app in a multizone VPC cluster by using Ingress](images/roks_router_ingress_vpc.png "Publicly expose an app in a multizone VPC cluster by using Ingress"){: caption="Figure 1. Publicly expose an app in a multizone VPC cluster by using Ingress" caption-side="bottom"}

1. A user sends a request to your app by accessing your app's URL. This URL is the Ingress subdomain for your cluster for your exposed app appended with the Ingress resource path, such as `mycluster-<hash>-0000.us-south.containers.appdomain.cloud/myapp`.

2. A DNS service resolves the route subdomain to the VPC load balancer hostname that is assigned to the Ingress controller. In VPC clusters, the external IP addresses are floating, and are kept behind a VPC-assigned hostname.

3. The VPC load balancer resolves the VPC hostname to an available IP address in a zone for the Ingress controller that was reported as healthy. The VPC load balancer continuously checks the external IP addresses for the Ingress controller in each zone in your cluster.

4. Based on the resolved IP address, the VPC load balancer sends the request to an Ingress controller.

5. The Ingress controller checks the routing rules that are implemented by the Ingress controller for the `myapp` path. If a matching rule is found, the request is proxied according to the rules that you defined in the IngressController and the Route resource to the pod where the app is deployed. The source IP address of the packet is changed to the IP address of the worker node where the Ingress controller pod runs. If multiple app instances are deployed in the cluster, the Ingress controller load balances the requests between the app pods across all zones.

6. When the app returns a response packet, it uses the IP address of the worker node where the Ingress controller service that forwarded the request exists. The VPC load balancer then sends the response packet to the client.


### VPC cluster with a private cloud service endpoint only
{: #architecture-vpc_private}

![VPC infrastructure provider icon.](images/icon-vpc-2.svg) When you create a multizone VPC cluster with the private cloud service endpoint only, a private Ingress controller is created by default. Only clients that are connected to your private VPC network can access apps that are exposed by a private Ingress controller. The following diagram shows how Ingress directs communication from private networks to an app in a VPC multizone cluster.
{: shortdesc}

![Privately expose an app in a multizone VPC cluster by using Ingress](images/roks_router_ingress_vpc_private.png "Privately expose an app in a multizone VPC cluster by using Ingress"){: caption="Figure 1. Privately expose an app in a multizone VPC cluster by using Ingress" caption-side="bottom"}

1. A client that is connected to your private VPC network sends a request to your app by using your app's URL. This URL is the Ingress subdomain for your cluster for your exposed app appended with the Ingress resource path, such as `mycluster-<hash>-i000.us-south.containers.appdomain.cloud/myapp`. For example, you might use the Virtual Private Cloud VPN, {{site.data.keyword.tg_full_notm}}, or {{site.data.keyword.dl_full_notm}} to allow requests from an on-premises network, another VPC, or {{site.data.keyword.cloud_notm}} classic infrastructure to apps that run in your cluster.

2. A DNS service resolves the route subdomain to the VPC load balancer hostname that is assigned to the services for the Ingress controller. In VPC clusters, your Ingress controller services' private IP addresses are floating, and are kept behind a VPC-assigned hostname. Note that though the DNS record for the route subdomain is registered in the public DNS system, the DNS resolution servers are reachable from the VPC.

3. The private VPC load balancer resolves the VPC hostname to an available private IP address of a Ingress controller service that was reported as healthy. The VPC load balancer continuously checks the IP addresses of the services that expose the Ingress controller in each zone in your cluster.

4. Based on the resolved IP address, the VPC load balancer sends the request to a Ingress controller service.

5. The Ingress controller checks the routing rules that are implemented by the Ingress controller for the `myapp` path. If a matching rule is found, the request is proxied according to the rules that you defined in the IngressController and the Route resource to the pod where the app is deployed. The source IP address of the packet is changed to the IP address of the worker node where the Ingress controller pod runs. If multiple app instances are deployed in the cluster, the Ingress controller load balances the requests between the app pods across all zones.

6. When the app returns a response packet, it uses the IP address of the worker node where the Ingress controller that forwarded the client request exists. The Ingress controller then sends the response packet through the VPC load balancer to the client.



## How can I customize routing?
{: #custom-routing}

If you want to customize routing rules for your app, you can use [route-specific HAProxy annotations](https://docs.openshift.com/container-platform/4.9/networking/routes/route-configuration.html#nw-route-specific-annotations_route-configuration){: external} that manages traffic for your app.

These supported annotations are in the format `haproxy.router.openshift.io/<annotation>` or `router.openshift.io/<annotation>`.

{{site.data.keyword.containerlong_notm}} annotations (`ingress.bluemix.net/<annotation>`) and NGINX annotations (`nginx.ingress.kubernetes.io/<annotation>`) are **not** supported for the Ingress controller, or the Route resource in {{site.data.keyword.redhat_openshift_notm}} version 4.

To get started, see [Customizing Ingress routing with annotations](/docs/openshift?topic=openshift-ingress-roks4#annotations-roks4).



## How can I enable TLS certificates?
{: #certs}

To load balance incoming HTTPS connections to your subdomain, you can configure the Ingress controller to decrypt the network traffic and forward the decrypted request to the apps that are exposed in your cluster.
{: shortdesc}

When you configure the public Ingress controller, you choose the domain that your apps are accessible through. If you use the IBM-provided domain, such as `mycluster-<hash>-0000.us-south.containers.appdomain.cloud/myapp`, you can use the default TLS certificate that is created for the Ingress subdomain. If you set up a CNAME record to map a custom domain to the IBM-provided domain, you can provide your own TLS certificate for your custom domain.

For more information about TLS certificates, see [Managing TLS certificates and secrets](/docs/openshift?topic=openshift-ingress-roks4#manage_certs).





