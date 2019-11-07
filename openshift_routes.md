---

copyright:
  years: 2014, 2019
lastupdated: "2019-11-06"

keywords: openshift, roks, rhoks, rhos, route, router

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
{:download: .download}
{:preview: .preview}

# Exposing apps with routes
{: #openshift_routes}

Use the router to publicly expose the services in your {{site.data.keyword.openshiftlong}} cluster on the router's external IP address by using a route.
{: shortdesc}

## Overview
{: #routes-overview}

A router is deployed by default to your cluster and functions as the ingress point for external network traffic. The router listens on the public host network interface, unlike your app pods that listen only on private IPs. The router uses the service selector to find the service and the endpoints that back the service, and creates [routes ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/architecture/networking/routes.html) that expose services as hostnames to be used by external clients. You can configure the service selector to direct traffic through one route to multiple services. You can also create either unsecured or secured routes by using the TLS certificate that is assigned by the router for your hostname. After you set up routes for your services, the router proxies external requests for route hostnames that you associate with services. Requests are sent to the IPs of the app pods that are identified by the service.

The route hostname for a service is formatted like `<service_name>-<namespace>.<cluster_name>-<random_hash>-0001.<region>.containers.appdomain.cloud`. Note that this hostname that is assigned to your route is different than the Ingress subdomain that is assigned by default to your cluster. Your route does not use the Ingress subdomain, but instead uses the router subdomain. You can find the router subdomain for your cluster by running `ibmcloud oc nlb-dns ls -c <cluster_name_or_ID>` and looking for the subdomain formatted like `<cluster_name>-<random_hash>-0001.<region>.containers.appdomain.cloud`.
{: note}

Not sure whether to use OpenShift routes or Ingress ALBs? Check out [Choosing among load balancing solutions](/docs/openshift?topic=openshift-network_planning#routes-vs-ingress).
{: tip}

## Setting up routes for your apps
{: #routes-setup}

To get started with routes to expose your apps:
{: shortdesc}

1. [Create a public or private service ![External link icon](../icons/launch-glyph.svg "External link icon")](https://kubernetes.io/docs/concepts/services-networking/service/#defining-a-service) so that the router can identify the endpoints for your app.

2. [Set up a route ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/dev_guide/routes.html).

3. Customize routing rules with [optional configurations ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/architecture/networking/routes.html).
