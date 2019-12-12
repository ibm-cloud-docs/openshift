---

copyright:
  years: 2014, 2019
lastupdated: "2019-12-12"

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

# About Ingress
{: #ingress-about-roks4}

Ingress is a service that balances network traffic workloads in your cluster by forwarding public or private requests to your apps. You can use Ingress to expose multiple app services to the public or to a private network by using a unique public or private domain.
{: shortdesc}

## What comes with Ingress?
{: #ingress_roks4_components}

In OpenShift version 4.3 and later clusters on Red Hat OpenShift on IBM Cloud, Ingress consists of three components: an Ingress controller, a router, and Ingress resources.
{: shortdesc}

### Ingress controller
{: #ingress-controller}

The [OpenShift Ingress controller ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/4.2/networking/ingress-operator.html) is a HAProxy-based Kubernetes service that you can use to expose apps in your cluster.
{: shortdesc}

When you deploy an app, the Ingress operator for your cluster creates an Ingress controller in the format `<name>`. This Ingress controller manages all incoming traffic for that app only by implementing routing rules for the app. The Ingress controller is registered with the default Ingress subdomain for your cluster in the format `<cluster_name>.<globally_unique_account_HASH>-0000.<region>.containers.appdomain.cloud`. If you want to register your app with a different domain, you can edit the Ingress controller for your app with your custom domain so that the controller implements routing rules for that domain instead.

To see the Ingress controller for your app, run `oc describe --namespace=openshift-ingress-operator ingresscontroller/<app_deployment_name>`.

### Router
{: #ingress-router}

When you deploy an app, the Ingress operator for your cluster creates an OpenShift router in the format `router-<ingress-controller-name>-<hash>`. The router listens for incoming HTTP, HTTPS, or TCP service requests, and then forwards requests to the pods for that app only according to the rules defined in the Ingress resource and implemented by the Ingress controller.
{: shortdesc}

You can find the IP address of each public router by running `oc get svc | grep router` and looking for the **EXTERNAL IP** field. The portable public and private router IP addresses are provisioned into your IBM Cloud infrastructure account during cluster creation and are static floating IPs that do not change for the life of the cluster. If the worker node is removed, a `Keepalived` daemon that constantly monitors the IP automatically reschedules the router pods that were on that worker to another worker node in that zone. The rescheduled router pods retain the same static IP address. However, if you remove a zone from a cluster, then the router IP address for that zone is removed.

Note that if you manually create a router, the router is not managed by the Ingress operator an is not registered with the Ingress subdomain or an app in your cluster.

### Ingress resource
{: #ingress-resource}

To expose an app by using Ingress, you must create a Kubernetes service for your app and register this service with the Ingress controller by defining an Ingress resource. The Ingress resource is a Kubernetes resource that defines the rules for how to route incoming requests for apps.
{: shortdesc}

The Ingress resource also specifies the path to your app services. The paths to your app services are appended to your cluster's Ingress subdomain to form a unique app URL such as `mycluster-a1b2cdef345678g9hi012j3kl4567890-0000.us-south.containers.appdomain.cloud/myapp1`.

One Ingress resource is required per namespace where you have apps that you want to expose.
* If the apps in your cluster are all in the same namespace, one Ingress resource is required to define routing rules for the apps that are exposed there. Note that if you want to use different domains for the apps within the same namespace, you can create one resource per domain.
* If the apps in your cluster are in different namespaces, you must create one resource per namespace to define rules for the apps that are exposed there.

For more information, see [Planning networking for single or multiple namespaces](/docs/containers?topic=containers-ingress#multiple_namespaces).

If you want to customize routing rules for your app, you can use [HAProxy annotations for the OpenShift router ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/architecture/networking/routes.html#route-specific-annotations) that manages traffic for your app. These annotation atre in the format `haproxy.router.openshift.io/<annotation>`. Note that {{site.data.keyword.containerlong_notm}} annotations (`ingress.bluemix.net/<annotation>`) and NGINX annotations (`nginx.ingress.kubernetes.io/<annotation>`) are not supported for the router or the Ingress resource in OpenShift version 4.3 and later.
{: important}

<br />


## How does a request get to my app with Ingress?
{: #roks4-flow}

### Single-zone cluster
{: #classic-single-roks4}

The following diagram shows how Ingress directs communication from the internet to an app in a classic single-zone cluster.
{: shortdesc}

<img src="/images/roks_router_ingress_single.png" width="600" alt="Expose an app in a single-zone cluster by using Ingress" style="width:600px; border-style: none"/>

1. A user sends a request to your app by accessing your app's URL. This URL is the Ingress subdomain for your cluster appended with the Ingress resource path for your exposed app, such as `mycluster-<hash>-0000.us-south.containers.appdomain.cloud/myapp`.

2. A DNS system service resolves the subdomain in the URL to the portable public IP address of the load balancer that exposes the router in your cluster.

3. Based on the resolved IP address, the client sends the request to the load balancer service that exposes the router.

4. The load balancer service routes the request to the router.

5. The router checks the routing rules that are implemented by the Ingress controller for a routing rule for the `myapp` path. If a matching rule is found, the request is proxied according to the rules that you defined in the router and the Ingress resource to the pod where the app is deployed. The source IP address of the package is changed to the IP address of the worker node where the app pod runs. If multiple app instances are deployed in the cluster, the router load balances the requests between the app pods.

6. When the app returns a response packet, it uses the IP address of the worker node where the router that forwarded the request exists. The router then sends the response packet to the client.

### Multizone cluster
{: #classic-multi-roks4}

The following diagram shows how Ingress directs communication from the internet to an app in a classic multizone cluster.
{: shortdesc}

<img src="images/images/roks_router_ingress_multizone.png" width="800" alt="Expose an app in a multizone cluster by using Ingress" style="width:800px; border-style: none"/>

1. A user sends a request to your app by accessing your app's URL. This URL is the Ingress subdomain for your cluster appended with the Ingress resource path for your exposed app, such as `mycluster-<hash>-0000.us-south.containers.appdomain.cloud/myapp`.

2. A DNS system service, which acts as the global load balancer, resolves the subdomain in the URL to the portable public IP address of the load balancer that exposes a router in one zone of the cluster. The IP addresses are resolved in a round-robin cycle, ensuring that requests are equally load balanced among the routers in various zones.

3. The client sends the request to the IP address of the load balancer service that exposes the router for your app.

4. The load balancer service routes the request to the router.

5. The router checks the routing rules that are implemented by the Ingress controller for a routing rule for the `myapp` path. If a matching rule is found, the request is proxied according to the rules that you defined in the router and the Ingress resource to the pod where the app is deployed. The source IP address of the package is changed to the IP address of the worker node where the app pod runs. If multiple app instances are deployed in the cluster, the router load balances the requests between the app pods across all zones.

6. When the app returns a response packet, it uses the IP address of the worker node where the router that forwarded the request exists. The router then sends the response packet to the client.
