---

copyright:
  years: 2014, 2020
lastupdated: "2020-04-06"

keywords: openshift, roks, rhoks, rhos, nginx, ingress controller, ingress operator, router

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


# About Ingress in OpenShift version 4.3
{: #ingress-about-roks4}

Ingress is a service that balances network traffic workloads in your cluster by forwarding public or private requests to your apps. You can use Ingress to expose multiple app services to the public or to a private network by using a unique public or private domain.
{: shortdesc}

<img src="images/icon-version-43.png" alt="Version 4.3 icon" width="30" style="width:30px; border-style: none"/> This information is for clusters that run OpenShift version 4.3 or later only. To learn about Ingress for OpenShift version 3.11 clusters, see [About Ingress in OpenShift version 3.11](/docs/openshift?topic=openshift-ingress-about).
{: note}

## What are the components of Ingress?
{: #ingress_roks4_components}

In clusters that run OpenShift version 4.3 or later, Ingress consists of three components: an Ingress controller, a router, and Ingress resources.
{: shortdesc}

### Ingress controller
{: #ingress-controller}

The [OpenShift Ingress controller](https://docs.openshift.com/container-platform/4.2/networking/ingress-operator.html){: external} implements routing rules that are applied to all incoming traffic for the apps in your cluster.
{: shortdesc}

Ingress controllers are managed by the Ingress operator. During cluster creation, the default Ingress controller is registered with the default Ingress subdomain for your cluster in the format `<cluster_name>.<globally_unique_account_HASH>-0000.<region>.containers.appdomain.cloud`. When you register your app with this subdomain by creating an Ingress resource, the Ingress controller ensures that requests to your app through this subdomain are properly proxied to your app pods. To see the default Ingress controller in your cluster, run `oc describe ingresscontroller/default -n openshift-ingress-operator`.

If you want to register your app with a different domain, you can [create a custom Ingress controller](/docs/openshift?topic=openshift-ingress-roks4#ingress-roks4-public-2) that implements routing rules for a custom domain instead.

### Router
{: #ingress-router}

One HAProxy-based OpenShift router is created for each Ingress controller, and one router service is created in each zone where you have worker nodes.
{: shortdesc}

The Ingress operator configures the router with the same domain that is specified in the Ingress controller. The router listens for incoming HTTP, HTTPS, or TCP service requests through that domain. The router's load balancer service component then forwards requests to the pods for that app only according to the rules defined in the Ingress resource and implemented by the Ingress controller.

To find the IP addresses of the default Ingress controller router services, run `oc get svc -n openshift-ingress` and look for the **EXTERNAL IP** field. If you have a multizone cluster, note that the router service in the first zone where you have workers nodes is always named `router-default`, and router services in the zones that you subsequently add to your cluster have names such as `router-dal12`.

If you manually create a router, the router is not managed by the Ingress operator and is not automatically registered with the Ingress subdomain or an app in your cluster.
{: note}

### Ingress resource
{: #ingress-resource-about}

To expose an app by using Ingress, you must create a Kubernetes service for your app and register this service with the Ingress controller by defining an Ingress resource. The Ingress resource is a Kubernetes resource that defines the rules for how to route incoming requests for apps.
{: shortdesc}

The Ingress resource also specifies the path to your app services. The paths to your app services are appended to your cluster's Ingress subdomain to form a unique app URL such as `mycluster-a1b2cdef345678g9hi012j3kl4567890-0000.us-south.containers.appdomain.cloud/myapp1`.

One Ingress resource is required for each project where you have apps that you want to expose.
* If the apps in your cluster are all in the same project, you must create one Ingress resource to define the routing rules for the apps that you want to expose. Note that if you want to use different domains for the apps within the same project, you can create one resource per domain.
* If the apps in your cluster are in different projects, you must create one Ingress resource for each project to define the app's routing rules.

For more information, see [Planning networking for single or multiple projects](/docs/openshift?topic=openshift-ingress#multiple_projects).

If you want to customize routing rules for your app, you can use [HAProxy annotations for the OpenShift router](/docs/openshift?topic=openshift-ingress-roks4#annotations-roks4) that manages traffic for your app. These supported annotations are in the format `haproxy.router.openshift.io/<annotation>`  or `router.openshift.io/<annotation>`. Note that {{site.data.keyword.containerlong_notm}} annotations (`ingress.bluemix.net/<annotation>`) and NGINX annotations (`nginx.ingress.kubernetes.io/<annotation>`) are not supported for the router or the Ingress resource in OpenShift version 4.3 and later.
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

3. Based on the resolved IP address, the client sends the request to the router service.

4. The router checks the routing rules that are implemented by the Ingress controller for a routing rule for the `myapp` path. If a matching rule is found, the request is proxied according to the rules that you defined in the router and the Ingress resource to the pod where the app is deployed. The source IP address of the package is changed to the IP address of the worker node where the app pod runs. If multiple app instances are deployed in the cluster, the router load balances the requests between the app pods.

5. When the app returns a response packet, it uses the IP address of the worker node where the router that forwarded the request exists. The router then sends the response packet to the client.

### Multizone cluster
{: #classic-multi-roks4}

The following diagram shows how Ingress directs communication from the internet to an app in a classic multizone cluster.
{: shortdesc}

<img src="/images/roks_router_ingress_multizone.png" width="800" alt="Expose an app in a multizone cluster by using Ingress" style="width:800px; border-style: none"/>

1. A user sends a request to your app by accessing your app's URL. This URL is the Ingress subdomain for your cluster appended with the Ingress resource path for your exposed app, such as `mycluster-<hash>-0000.us-south.containers.appdomain.cloud/myapp`.

2. A DNS system service, which acts as the global load balancer, resolves the subdomain in the URL to the portable public IP address of a router service in one zone of the cluster. The IP addresses are resolved in a round-robin cycle, ensuring that requests are equally load balanced among the routers in various zones.

3. The client sends the request to the IP address of the service that exposes the router.

4. The router checks the routing rules that are implemented by the Ingress controller for the `myapp` path. If a matching rule is found, the request is proxied according to the rules that you defined in the router and the Ingress resource to the pod where the app is deployed. The source IP address of the package is changed to the IP address of the worker node where the app pod runs. If multiple app instances are deployed in the cluster, the router service sends the requests between the app pods across all zones.

5. When the app returns a response packet, it uses the IP address of the worker node where the router service that forwarded the request exists. The router then sends the response packet to the client.
