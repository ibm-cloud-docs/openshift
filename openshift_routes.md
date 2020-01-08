---

copyright:
  years: 2014, 2020
lastupdated: "2020-01-08"

keywords: openshift, roks, rhoks, rhos, route, router

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


# Exposing apps with routes
{: #openshift_routes}

Use the router to publicly expose the services in your {{site.data.keyword.openshiftlong}} cluster on the router's external IP address by using a route.
{: shortdesc}

## Overview
{: #routes-overview}

A router is deployed by default to your cluster and functions as the ingress point for external network traffic. The router listens on the public host network interface, unlike your app pods that listen only on private IPs. The router uses the service selector to find the service and the endpoints that back the service, and creates [routes ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/architecture/networking/routes.html) that expose services as hostnames to be used by external clients. You can configure the service selector to direct traffic through one route to multiple services. You can also create either unsecured or secured routes by using the TLS certificate that is assigned by the router for your hostname. After you set up routes for your services, the router proxies external requests for route hostnames that you associate with services. Requests are sent to the IPs of the app pods that are identified by the service.

The route hostname for a service is formatted like `<service_name>-<project>.<cluster_name>-<random_hash>-0001.<region>.containers.appdomain.cloud`. Note that this hostname that is assigned to your route is different than the Ingress subdomain that is assigned by default to your cluster. You can find the router subdomain for your cluster by running `ibmcloud oc nlb-dns ls -c <cluster_name_or_ID>` and looking for the subdomain formatted like `<cluster_name>-<random_hash>-0001.<region>.containers.appdomain.cloud`.
{: note}

Not sure whether to use OpenShift routes or Ingress ALBs? Check out [Choosing among load balancing solutions](/docs/openshift?topic=openshift-cs_network_planning#routes-vs-ingress).
{: tip}

The following diagram shows how a router directs communication from the internet to an app.

<img src="images/roks-router.png" alt="Expose an app in a single-zone OpenShift cluster by using a router" width="550" style="width:550px; border-style: none"/>

1. A request to your app uses the route hostname that you set up for your app. A DNS system service resolves the subdomain to the floating public IP address of the load balancer service that exposes the router.

2. The router receives the request and forwards it to the private IP address of the app pod over the private network. The source IP address of the request package is changed to the public IP address of the worker node where the router pod runs. If multiple app instances are deployed in the cluster, the router sends the requests between the app pods.

3. When the app returns a response packet, it uses the IP address of the worker node where the router that forwarded the client request exists. The router then sends the response packet through the load balancer service to the client.

## Setting up routes to publicly expose your apps
{: #routes-setup}

To set up routes to publicly expose apps:
{: shortdesc}

1. Create a Kubernetes `ClusterIP` service for your app deployment. The service provides an internal IP address for the app that the router can send traffic to.
  ```
  oc expose deploy <app_deployment_name> --name my-app-svc
  ```
  {: pre}

2. Choose a domain for your app.
  * IBM-provided domain: If you do not need to use a custom domain, a subdomain is generated for you in the format `<service_name>-<project>.<cluster_name>-<random_hash>-0001.<region>.containers.appdomain.cloud`.
  * Custom domain: To specify a custom domain, work with your DNS provider or [{{site.data.keyword.cis_full}}](https://cloud.ibm.com/catalog/services/internet-services).
    1. Get the public IP address for the router in the **EXTERNAL-IP** column.
      ```
      oc get svc router
      ```
      {: pre}
    2. Create a custom domain with your DNS provider.
        If you want to use the same subdomain for multiple services in your cluster, you can register a wildcard subdomain, such as `*.example.com`.
        {: tip}
    3. Map your custom domain to the router's public IP address by adding the IP address as an A record.

3. [Set up a route ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/dev_guide/routes.html).
  * If you do not have a custom domain, leave the **Hostname** field blank.
  * If you registered a wildcard subdomain, specify a unique subdomain in each route resource that you create. For example, you might specify `svc1.example.com` in this route resource, and `svc2.example.com` in another route resource.

4. Customize the default routing rules with [optional configurations ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/architecture/networking/routes.html).

You can list the routes in your cluster at any time by running `oc get routes`.
{: tip}

<br />


## Setting up routes to privately expose your apps
{: #private-routes-setup}

To use routes to privately expose your apps, create a new router and change the service that exposes the router to a private load balancer. The router is assigned an IP address through which private requests are forwarded to your app.
{: shortdesc}

1. Create a Kubernetes `ClusterIP` service for your app deployment. The service provides an internal IP address for the app that the router can send traffic to.
  ```
  oc expose deploy <app_deployment_name> --name my-app-svc -n <project>
  ```
  {: pre}

2. Create a router that is named `router-private`.
  ```
  oc adm router router-private --replicas=2 --service-account=router -n <project>
  ```
  {: pre}

3. Change the `router-private` service that exposes the router to a private load balancer.
  1. Edit the `router-private` service.
    ```
    oc edit svc router-private -n <project>
    ```
    {: pre}
  2. In the `metadata.annotations` section, add the `service.kubernetes.io/ibm-load-balancer-cloud-provider-ip-type: private` annotation.
  3. In the `spec.ports` section, change the default `80` and `443` ports that are used by the default public router to other ports, such as `8080` and `8443`.
  3. Change `spec.type` to `LoadBalancer`.
  4. Save and close the file. After you finish editing the file, it looks similar to the following:
      ```
      apiVersion: v1
      kind: Service
      metadata:
        annotations:
          prometheus.openshift.io/password: S5ALaAB5d3
          prometheus.openshift.io/username: admin
          service.alpha.openshift.io/serving-cert-secret-name: router-private-certs
          service.alpha.openshift.io/serving-cert-signed-by: openshift-service-serving-signer
          service.kubernetes.io/ibm-load-balancer-cloud-provider-ip-type: private
        labels:
          router: router-private
        name: router-private
        namespace: default
      spec:
        ports:
        - name: 8080-tcp
          port: 8080
          protocol: TCP
          targetPort: 8080
        - name: 8443-tcp
          port: 8443
          protocol: TCP
          targetPort: 8443
        - name: 1936-tcp
          port: 1936
          protocol: TCP
          targetPort: 1936
        selector:
          router: router-private
        sessionAffinity: None
        type: LoadBalancer
      ```
      {: codeblock}

4. Update the project where your app deployment, service, and router are deployed to use the private router instead of the default public router.
  ```
  oc label namespace <project> "router=router-private"
  ```
  {: pre}

5. Restart the pods for the private router.
  ```
  oc scale dc/router-private --replicas=0 -n <project> && oc scale dc/router-private --replicas=2 -n <project>
  ```
  {: pre}

6. [Set up a route ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/dev_guide/routes.html). Leave the **Hostname** field blank.

7. Customize the default routing rules with [optional configurations ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/architecture/networking/routes.html).

You can list the routes in your cluster at any time by running `oc get routes`.
{: tip}
