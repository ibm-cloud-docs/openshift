---

copyright:
  years: 2014, 2020
lastupdated: "2020-06-09"

keywords: openshift, roks, rhoks, rhos, route, router

subcollection: openshift

---

{:beta: .beta}
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
{: help}
{: support}

Use the router to publicly expose the services in your {{site.data.keyword.openshiftlong}} cluster on the router's external IP address by using a route.
{: shortdesc}

Not sure whether to use OpenShift routes or Ingress? Check out [Choosing among load balancing solutions](/docs/openshift?topic=openshift-cs_network_planning#routes-vs-ingress).
{: tip}

## Overview
{: #routes-overview}

A router is deployed by default to your cluster and functions as the ingress point for external network traffic. The router listens on the public host network interface, unlike your app pods that listen only on private IPs. The router uses the service selector to find the service and the endpoints that back the service, and creates [routes](https://docs.openshift.com/container-platform/4.3/networking/routes/route-configuration.html){: external} that expose services as hostnames to be used by external clients. You can configure the service selector to direct traffic through one route to multiple services. You can also create either unsecured or secured routes by using the TLS certificate that is assigned by the router for your hostname. After you set up routes for your services, the router proxies external requests for route hostnames that you associate with services. Requests are sent to the IPs of the app pods that are identified by the service.

If you have a multizone cluster, one router is deployed to your cluster, and a router service is created in each zone. Note that the router service in the first zone where you have workers nodes is always named `router-default` in 4.3 clusters or `router` in 3.11 clusters, and router services in zones that you subsequently add to your cluster have names such as `router-dal12`.
* To see the router services in each zone of your cluster, run `oc get svc -n openshift-ingress`.
* To see the router subdomain for your cluster and the IP addresses for the router service in each zone, run `ibmcloud oc nlb-dns ls -c <cluster_name_or_ID>` and looking for the subdomain formatted like `<cluster_name>-<random_hash>-0000.<region>.containers.appdomain.cloud`.

### Traffic flow in a single-zone cluster
{: #route_single}

The following diagram shows how a router directs network traffic from the internet to an app in a single-zone cluster.
{: shortdesc}

<img src="images/roks-router.png" alt="Expose an app in a single-zone OpenShift cluster by using a router" width="550" style="width:550px; border-style: none"/>

1. A request to your app uses the route hostname that you set up for your app. A DNS system service resolves the subdomain to the floating public IP address of router service.

2. The router service receives the request and forwards it to the private IP address of the app pod over the private network. The source IP address of the request package is changed to the public IP address of the worker node where the router pod runs. If multiple app instances are deployed in the cluster, the router sends the requests between the app pods.

3. When the app returns a response packet, it uses the IP address of the worker node where the router that forwarded the client request exists. The router then sends the response packet through the load balancer service to the client.

### Traffic flow in a multizone cluster
{: #route_multi}

The following diagram shows how a router directs network traffic from the internet to an app in a multizone cluster.
{: shortdesc}

<img src="images/roks-router-multi.png" alt="Expose an app in a multizone OpenShift cluster by using a router" width="700" style="width:700px; border-style: none"/>

1. A request to your app uses the route hostname that you set up for your app.

2. A DNS system service resolves the route subdomain to the floating public IP address of a router service that was reported as healthy by the MZLB. The MZLB continuously checks the portable public IP addresses of the services that expose the router in each zone in your cluster. Requests are handled by the router services in various zones in a round-robin cycle.

3. The router receives the request and forwards it to the private IP address of the app pod over the private network. The source IP address of the request package is changed to the public IP address of the worker node where the router pod runs. Each router sends requests to the app instances in its own zone and to app instances in other zones. Additionally, if multiple app instances are deployed in one zone, the router sends the requests between the app pods in the zone.

4. When the app returns a response packet, it uses the IP address of the worker node where the router that forwarded the client request exists. The router then sends the response packet through the load balancer service to the client.

<br />


## Route types
{: #route-types}

OpenShift offers four types of routes based on the type of TLS termination that your app requires. Each route type is supported for public and private routes and for version 3.11 and 4.3 clusters.
{: shortdesc}

| Route type | Use case |
| ---------- | -------- |
| Simple | When no TLS encryption is involved, create a simple route to handle non-encrypted HTTP traffic. |
| Passthrough | When you want TLS connections to pass from the client to your app pod uninterrupted, create a passthrough route. The router is not involved in TLS termination for encrypted HTTPS traffic, so the app pod must terminate the TLS connection. This type can also be used for HTTP/2 and for non-HTTP TLS endpoints. |
| Edge | When your app pod is exposed on a non-encrypted HTTP endpoint, but you must handle encrypted HTTPS traffic, create an edge route. The TLS connection between the client and the router service is terminated, and the connection between the router service and your app pod is unencrypted. For more information, see the [OpenShift edge route documentation](https://docs.openshift.com/container-platform/4.3/networking/routes/secured-routes.html#nw-ingress-creating-an-edge-route-with-a-custom-certificate_secured-routes){: external}. |
| Re-encrypt | When your app pod is exposed on an encrypted HTTPS endpoint and you must handle HTTPS traffic, create a re-encrypt route. The TLS connection between the client and the router service is terminated, and a new TLS connection between the router service and your app pod is created. For more information, see the [OpenShift re-encrypt route documentation](https://docs.openshift.com/container-platform/4.3/networking/routes/secured-routes.html#nw-ingress-creating-a-reencrypt-route-with-a-custom-certificate_secured-routes){: external}. |
{: caption="Types of routes based on TLS termination"}

## Setting up public routes
{: #routes-setup}

To set up routes to publicly expose apps in version 4.3 and 3.11 clusters:
{: shortdesc}

1. Create a Kubernetes `ClusterIP` service for your app deployment. The service provides an internal IP address for the app that the router can send traffic to.
  ```
  oc expose deploy <app_deployment_name> --name my-app-svc
  ```
  {: pre}

2. Choose a domain for your app.
  * **IBM-provided domain**: If you do not need to use a custom domain, a route subdomain is generated for you in the format `<service_name>-<project>.<cluster_name>-<random_hash>-0000.<region>.containers.appdomain.cloud`.
  * **Custom domain**: To specify a custom domain, work with your DNS provider or [{{site.data.keyword.cis_full}}](https://cloud.ibm.com/catalog/services/internet-services).
    1. Get the public IP address for the public router service in each zone in the **EXTERNAL-IP** column. Note that the router service in the first zone where you have workers nodes is always named `router-default` in 4.3 clusters or `router` in 3.11 clusters, and router services in zones that you subsequently add to your cluster have names such as `router-dal12`.
      * Version 4.3 and later clusters:
        ```
        oc get svc -n openshift-ingress
        ```
        {: pre}
      * Version 3.11 clusters:
        ```
        oc get svc router
        ```
        {: pre}
    2. Create a custom domain with your DNS provider.
        If you want to use the same subdomain for multiple services in your cluster, you can register a wildcard subdomain, such as `*.example.com`.
        {: tip}
    3. Map your custom domain to the router's public IP address by adding the IP address as an A record.

3. Set up a route that is based on the [type of TLS termination that your app requires](#route-types). If you do not have a custom domain, do not include the `--hostname` flag. A route subdomain is generated for you in the format `<service_name>-<project>.<cluster_name>-<random_hash>-0000.<region>.containers.appdomain.cloud`. If you registered a wildcard subdomain, specify a unique subdomain in each route that you create. For example, you might specify `--hostname svc1.example.com` in this route, and `--hostname svc2.example.com` in another route.
    * Simple:
      ```
      oc expose service <app_service_name> [--hostname <subdomain>]
      ```
      {: pre}
    * Passthrough:
      ```
      oc create route passthrough --service <app_service_name> [--hostname <subdomain>]
      ```
      {: pre}
      <p class="tip">Need to handle HTTP/2 connections? After you create the route, run `oc edit route <app_service_name>` and change the route's `targetPort` value to `https`. You can test the route by running `curl -I --http2 https://<route> --insecure`.</p>
    * Edge: For more information about the TLS certificate requirements, see the [OpenShift edge route documentation](https://docs.openshift.com/container-platform/4.3/networking/routes/secured-routes.html#nw-ingress-creating-an-edge-route-with-a-custom-certificate_secured-routes){: external}.
      ```
      oc create route edge --service <app_service_name> --cert <tls.crt> --key <tls.key> --ca-cert <ca.crt> [--hostname <subdomain>]
      ```
      {: pre}
    * Re-encrypt: For more information about the TLS certificate requirements, see the [OpenShift re-encrypt route documentation](https://docs.openshift.com/container-platform/4.3/networking/routes/secured-routes.html#nw-ingress-creating-a-reencrypt-route-with-a-custom-certificate_secured-routes){: external}.
      ```
      oc create route reencrypt --service <app_service_name> --cert <tls.crt> --key <tls.key> --dest-ca-cert <destca.crt> --ca-cert <ca.crt> [--hostname <subdomain>]
      ```
      {: pre}

4. Verify that the route for your app service is created.
  ```
  oc get routes
  ```
  {: pre}

5. Optional: Customize default routing rules with [optional configurations](https://docs.openshift.com/container-platform/4.3/networking/routes/route-configuration.html){: external}. For example, you can use [HAProxy annotations for the OpenShift router](https://docs.openshift.com/container-platform/4.3/networking/routes/route-configuration.html#nw-route-specific-annotations_route-configuration){: external}.

<br />


## Setting up private routes
{: #private-routes}

Use routes to expose your apps on private networks.
{: shortdesc}

### Setting up private routes in 4.3 clusters
{: #private-routes-setup-43}

To use routes to privately expose your apps in version 4.3 clusters, you must create a private Ingress controller and configure the controller with a custom subdomain that you provide. The Ingress controller automatically creates and configures a new private router, which you can use to create private routes for your apps.
{: shortdesc}

1. Create a custom domain. To register your custom domain, work with your Domain Name Service (DNS) provider or [{{site.data.keyword.cloud_notm}} DNS](/docs/dns?topic=dns-getting-started). Note that you cannot use the default public subdomain for your cluster.<p class="tip">If you want to use the same subdomain for multiple services in your cluster, you can register a wildcard subdomain, such as `*.example.com`.</p>

2.  Create a configuration file that configures a private Ingress controller with your custom domain.
    ```yaml
    apiVersion: operator.openshift.io/v1
    kind: IngressController
    metadata:
      name: private
      namespace: openshift-ingress-operator
    spec:
      replicas: 2
      domain: <custom_domain>
      endpointPublishingStrategy:
        loadBalancer:
          scope: Internal
        type: LoadBalancerService
    ```
    {: codeblock}

3. Create the Ingress controller in the `openshift-ingress-operator` namespace of your cluster. When you create the Ingress controller, a private router is automatically created and deployed in the `openshift-ingress` namespace based on the Ingress controller settings. Additionally, a router service is created to expose the router with an IP address.
  ```
  oc create -f private.yaml -n openshift-ingress-operator
  ```
  {: pre}

4.  Get the **EXTERNAL IP** field of the `router-private` service.
  ```
  oc get svc router-private -n openshift-ingress
  ```
  {: pre}

  Example output:
  ```
  NAME                          TYPE           CLUSTER-IP       EXTERNAL-IP    PORT(S)                      AGE
  router-private                LoadBalancer   172.21.57.132    10.XX.XX.XX    80/TCP,443/TCP,1940/TCP      3m
  ```
  {: screen}

5. Work with your DNS provider to add the service's external IP address as an A record that maps to your custom domain.

6. Update the project where your app is deployed to use the private router instead of the default public router.
  ```
  oc label namespace <app_project> "router=router-private"
  ```
  {: pre}

7. Create a Kubernetes `ClusterIP` service for your app deployment. The service provides an internal IP address for the app that the router can send traffic to.
  ```
  oc expose deploy <app_deployment_name> --name <app_service_name> -n <app_project>
  ```
  {: pre}

8. Set up a route that is based on the [type of TLS termination that your app requires](#route-types). If you do not include the `--hostname` flag, a route hostname is generated for you in the format `<app_service_name>-<app_project>.<custom_domain>`. If you registered a wildcard subdomain, specify a unique subdomain in each route that you create. For example, you might specify `--hostname svc1.example.com` in this route, and `--hostname svc2.example.com` in another route.
    * Simple:
      ```
      oc expose service <app_service_name> [--hostname <subdomain>]
      ```
      {: pre}
    * Passthrough:
      ```
      oc create route passthrough --service <app_service_name> [--hostname <subdomain>]
      ```
      {: pre}
      <p class="tip">Need to handle HTTP/2 connections? After you create the route, run `oc edit route <app_service_name>` and change the route's `targetPort` value to `https`. You can test the route by running `curl -I --http2 https://<route> --insecure`.</p>
    * Edge: For more information about the TLS certificate requirements, see the [OpenShift edge route documentation](https://docs.openshift.com/container-platform/4.3/networking/routes/secured-routes.html#nw-ingress-creating-an-edge-route-with-a-custom-certificate_secured-routes){: external}.
      ```
      oc create route edge --service <app_service_name> --cert <tls.crt> --key <tls.key> --ca-cert <ca.crt> [--hostname <subdomain>]
      ```
      {: pre}
    * Re-encrypt: For more information about the TLS certificate requirements, see the [OpenShift re-encrypt route documentation](https://docs.openshift.com/container-platform/4.3/networking/routes/secured-routes.html#nw-ingress-creating-a-reencrypt-route-with-a-custom-certificate_secured-routes){: external}.
      ```
      oc create route reencrypt --service <app_service_name> --cert <tls.crt> --key <tls.key> --dest-ca-cert <destca.crt> --ca-cert <ca.crt> [--hostname <subdomain>]
      ```
      {: pre}

9. Verify that the route for your app is created.
  ```
  oc get routes
  ```
  {: pre}

10. Optional: Customize the private router's routing rules with [optional configurations](https://docs.openshift.com/container-platform/4.3/networking/routes/route-configuration.html){: external}. For example, you can use [HAProxy annotations for the OpenShift router](https://docs.openshift.com/container-platform/4.3/networking/routes/route-configuration.html#nw-route-specific-annotations_route-configuration){: external}.

11. To create routes for more apps by using the same subdomain, you can repeat steps 7 - 10 so that the route is generated by the same private router. If you want to create routes for more apps by using a different subdomain, repeat all steps in this section to create a new private router.

### Setting up private routes in 3.11 clusters
{: #private-routes-setup}

To use routes to privately expose your apps in version 3.11 clusters, create a new router and change the service that exposes the router to a private load balancer. The router service is assigned an IP address through which private requests are forwarded to your app.
{: shortdesc}

When you create a private router, the private router uses host networking to listen on the ports that you specify. Ensure that no other services that use host networking in your cluster listen on these ports.
{: important}

1. Create a router that is named `router-private` in the project where your app is deployed. A service that exposes the private router is also automatically created.
  ```
  oc adm router router-private --replicas=2 --service-account=router --images registry.ng.bluemix.net/armada-master/iksorigin-ose-haproxy-router:v3.11.154 -n <project>
  ```
  {: pre}

2. Change the ports of the deployment configuration for the private router. You must change these ports because the default ports are already used by the default public router for your cluster.
  1. Edit the `router-private` deployment configuration.
      ```
      oc edit dc router-private -n <project>
      ```
      {: pre}
  2. In the `spec.containers.env` section, change the values of `ROUTER_SERVICE_HTTPS_PORT` and `ROUTER_SERVICE_HTTP_PORT` to other ports, such as to `8443` and `8080`. Note that the private router uses host networking to listen on the ports that you choose, so ensure that no other services that use host networking listen on these ports.
  3. In the `spec.containers.env.ports` section, change the default `80` and `443` ports to the same ports that you specified in the previous step.
  4. Save and close the file.

3. Verify that the pods for the private router are re-created and have a **STATUS** of `Running`.
  ```
  oc get pods -n <project>
  ```
  {: pre}

  Example output:
  ```
  NAME                                READY     STATUS      RESTARTS   AGE
  ...
  router-private-2-5ftqh              1/1       Running     0          2m
  router-private-2-ksknz              1/1       Running     0          2m
  ```
  {: screen}

4. Change the `router-private` service that exposes the router to a private load balancer.
  1. Edit the `router-private` service.
    ```
    oc edit svc router-private -n <project>
    ```
    {: pre}
  2. In the `metadata.annotations` section, add the `service.kubernetes.io/ibm-load-balancer-cloud-provider-ip-type: private` annotation.
  3. In the `spec.ports` section, change the default `80` and `443` ports to the same ports that you specified in the deployment config for the private router.
  3. Change `spec.type` to `LoadBalancer`.
  4. Save and close the file. After you finish editing the file, it looks similar to the following:
      ```yaml
      apiVersion: v1
      kind: Service
      metadata:
        annotations:
          prometheus.openshift.io/password: xxxxxxxxxx
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

5. Verify that the `router-private` service has a **TYPE** of `LoadBalancer` and note the **EXTERNAL-IP** address.
    ```
    oc get svc router-private -n <project>
    ```
    {: pre}

    Example output:
    ```
    NAME                     TYPE           CLUSTER-IP       EXTERNAL-IP     PORT(S)                                     AGE
    router-private           LoadBalancer   172.21.XXX.XX    10.XX.XX.XX     80:31554/TCP,443:30329/TCP,1936:32477/TCP   2m
    ```
    {: screen}

6. To have an external endpoint for your private router, you must register your private router service's external IP address with a custom domain.
    1. Create a custom domain. To register your custom domain, work with your Domain Name Service (DNS) provider or [{{site.data.keyword.cloud_notm}} DNS](/docs/dns?topic=dns-getting-started).<p class="tip">If you want to use the same subdomain for multiple services in your cluster, you can register a wildcard subdomain, such as `*.example.com`.</p>
    2. Map your custom domain to the private router service's external IP address by adding the IP address as an A record.

7. Update the project where your app and private router are deployed to use the private router instead of the default public router.
  ```
  oc label namespace <project> "router=router-private"
  ```
  {: pre}

8. Restart the pods for the private router.
  ```
  oc scale dc/router-private --replicas=0 -n <project> && oc scale dc/router-private --replicas=2 -n <project>
  ```
  {: pre}

9. Create a Kubernetes `ClusterIP` service for your app deployment. The service provides an internal IP address for the app that the router can send traffic to.
  ```
  oc expose deploy <app_deployment_name> --name <app_service_name>
  ```
  {: pre}

10. Set up a route. If you do not specify a **Hostname** value and you registered the router service with a private DNS entry in step 6, a route hostname is generated for you in the format `<app_service_name>-<project>.<custom_domain>`.
  ```
  oc expose service <app_service_name>
  ```
  {: pre}

11. Verify that the route for your app is created.
  ```
  oc get routes
  ```
  {: pre}

12. Optional: Customize the private router's routing rules with [optional configurations](https://docs.openshift.com/container-platform/3.11/architecture/networking/routes.html){: external}. For example, you can use [HAProxy annotations for the OpenShift router](https://docs.openshift.com/container-platform/3.11/architecture/networking/routes.html#route-specific-annotations){: external}.

13. To create routes for more apps by using the same subdomain, you can repeat steps 9 - 12 so that the route is generated by the same private router. If you want to create routes for more apps by using a different subdomain, repeat all steps in this section to create a new private router.

## Moving router services across VLANs
{: #migrate-router-vlan}

When you [change your worker node VLAN connections](/docs/openshift?topic=openshift-cs_network_cluster#change-vlans), the worker nodes are connected to the new VLAN and assigned new public or private IP addresses. However, router services cannot automatically migrate to the new VLAN because they are assigned a stable, portable public or private IP address from a subnet that belongs to the old VLAN. When your worker nodes and routers are connected to different VLANs, the routers cannot forward incoming network traffic to app pods to your worker nodes. To move your router services to a different VLAN, you must create the router service on the new VLAN and delete the router service on the old VLAN.
{: shortdesc}

### Moving router services across VLANs in 4.3 clusters
{: #migrate-router-vlan-43}

Move router services across VLANs in version 4.3 and later clusters.
{: shortdesc}

1. Create a router service on the new VLAN.
    1. Create a YAML configuration file for a new router service. Specify the zone that the router service deploys to. Save the file as `router-new-<zone>.yaml`.
        * Public router service:
          ```yaml
          apiVersion: v1
          kind: Service
          metadata:
            annotations:
              service.kubernetes.io/ibm-load-balancer-cloud-provider-zone: <zone>
              service.kubernetes.io/ibm-load-balancer-cloud-provider-ip-type: public
            finalizers:
            - service.kubernetes.io/load-balancer-cleanup
            labels:
              app: router
              ingresscontroller.operator.openshift.io/deployment-ingresscontroller: default
              router: router-default
            name: router-new-<zone>
            namespace: openshift-ingress
          spec:
            externalTrafficPolicy: Local
            ports:
            - name: http
              port: 80
              protocol: TCP
              targetPort: http
            - name: https
              port: 443
              protocol: TCP
              targetPort: https
            selector:
              ingresscontroller.operator.openshift.io/deployment-ingresscontroller: default
            sessionAffinity: None
            type: LoadBalancer
          ```
          {: codeblock}
        * Private router service:
          ```yaml
          apiVersion: v1
          kind: Service
          metadata:
            annotations:
              service.kubernetes.io/ibm-load-balancer-cloud-provider-zone: <zone>
              service.kubernetes.io/ibm-load-balancer-cloud-provider-ip-type: private
            finalizers:
            - service.kubernetes.io/load-balancer-cleanup
            labels:
              app: router
              ingresscontroller.operator.openshift.io/deployment-ingresscontroller: private
              router: router-private
            name: router-new-<zone>
            namespace: openshift-ingress
          spec:
            externalTrafficPolicy: Local
            ports:
            - name: http
              port: 80
              protocol: TCP
              targetPort: http
            - name: https
              port: 443
              protocol: TCP
              targetPort: https
            selector:
              ingresscontroller.operator.openshift.io/deployment-ingresscontroller: private
            sessionAffinity: None
            type: LoadBalancer
          ```
          {: codeblock}

    2. Create the new router service.
      ```
      oc apply -f router-new-<zone>.yaml -n openshift-ingress
      ```
      {: pre}

    3. Get the **EXTERNAL-IP** address of the new router service. This IP address is from a subnet on the new VLAN.
      ```
      oc get svc router-new -n openshift-ingress
      ```
      {: pre}

      Example output for a public router service:
      ```
      NAME                         TYPE           CLUSTER-IP       EXTERNAL-IP     PORT(S)                                     AGE
      router-new                   LoadBalancer   172.21.XX.XX     169.XX.XXX.XX   80:31049/TCP,443:30219/TCP                  2m
      ```
      {: screen}

    4. **Multizone clusters**: If you changed the VLANs for worker nodes in multiple zones, repeat these steps to create a router service on the new VLANs in each zone.

2. Note the **Hostname** of the router. In the output, look for the hostname formatted like `<cluster_name>-<random_hash>-0001.<region>.containers.appdomain.cloud`.
  ```
  ibmcloud oc nlb-dns ls -c <cluster_name_or_ID>
  ```
  {: pre}

  Example output:
  ```
  Hostname                                                                             IP(s)           Health Monitor   SSL Cert Status   SSL Cert Secret Name                            Secret Namespace
  mycluster-35366fb2d3d90fd50548180f69e7d12a-0001.us-east.containers.appdomain.cloud   169.XX.XXX.XX   None             created           roks-ga-35366fb2d3d90fd50548180f69e7d12a-0001   default
  ...
  ```
  {: screen}

3. Add the IP address of the new router service that you found in step 1 to the router's hostname. If you created services for multiple zones in step 1, include each IP address separately in repeated `--ip` flags.
  ```
  ibmcloud oc nlb-dns add -c <cluster_name_or_ID> --ip <new_IP> --nlb-host <subdomain>
  ```
  {: pre}
  Your router service on the new VLAN is now registered with the domain for the default router in your cluster, and can forward incoming requests to apps.

4. Get the IP address of the old router service on the old VLAN. **Multizone clusters**: If you changed the VLANs for worker nodes in multiple zones, get the IP address for the router service in each zone where the VLANs changed. Note that the router service in the first zone where you have workers nodes is always named `router-default`, and router services in the zones that you subsequently add to your cluster have names such as `router-dal12`.
    ```
    oc get svc -n openshift-ingress
    ```
    {: pre}

    Example output for a multizone cluster:
    ```
    NAME                          TYPE           CLUSTER-IP       EXTERNAL-IP      PORT(S)                      AGE
    router-dal12                  LoadBalancer   172.21.190.62    169.XX.XX.XX     80:32318/TCP,443:30915/TCP   51d
    router-default                LoadBalancer   172.21.47.119    169.XX.XX.XX     80:31311/TCP,443:32561/TCP   78d
    router-internal-default       ClusterIP      172.21.51.30     <none>           80/TCP,443/TCP,1936/TCP      78d
    ```
    {: screen}

5. Remove the IP address of the old router service that you found in step 2 from the router's hostname. For multizone clusters, include each IP address separately in repeated `--ip` flags.
  ```
  ibmcloud oc nlb-dns rm classic -c <cluster_name_or_ID> --ip <old_IP> --nlb-host <hostname>
  ```
  {: pre}

6. Verify that the hostname for your router is now registered with the new IP address. After your router hostname is updated with the IP address of the new service, no further changes to your router or routes are required.
  ```
  ibmcloud oc nlb-dns ls -c <cluster_name_or_ID>
  ```
  {: pre}

7. Delete the router service on the old VLAN.
    ```
    oc delete svc <old_router_svc> -n openshift-ingress
    ```
    {: pre}

8. Optional: If you no longer need the subnets on the old VLANs, you can [remove them](/docs/openshift?topic=openshift-subnets#remove-subnets).


### Moving router services across VLANs in 3.11 clusters
{: #migrate-router-vlan-311}

Move router services across VLANs in version 3.11 clusters.
{: shortdesc}

1. Create a router service on the new VLAN.
    1. Describe the configuration for the default public router service. In the output, copy the `prometheus.openshift.io/password: xxxxxxxxxx` annotation, and any custom annotations that you manually added to the router. Do not copy other annotations.<p class="note">Note that the router service in the first zone where you have workers nodes is always named `router` in 3.11 clusters, and router services in the zones that you subsequently add to your cluster have names such as `router-dal12`.</p>
      ```
      oc get svc router -o yaml
      ```
      {: pre}

    2. Create a YAML configuration file for a new router service.
        1. Add the Prometheus password annotation and any custom annotations.
        2. Specify the zone that your router service deploys to.
        3. Save the file as `router-new.yaml`.
          ```yaml
          apiVersion: v1
          kind: Service
          metadata:
            annotations:
              prometheus.openshift.io/password: # your password
              prometheus.openshift.io/username: admin
              service.alpha.openshift.io/serving-cert-secret-name: router-certs
              service.alpha.openshift.io/serving-cert-signed-by: openshift-service-serving-signer
              service.kubernetes.io/ibm-load-balancer-cloud-provider-zone: <zone>
              service.kubernetes.io/ibm-load-balancer-cloud-provider-ip-type: public
            labels:
              router: router
            name: router-new
            namespace: default
          spec:
            externalTrafficPolicy: Cluster
            ports:
            - name: 80-tcp
              port: 80
              protocol: TCP
              targetPort: 80
            - name: 443-tcp
              port: 443
              protocol: TCP
              targetPort: 443
            selector:
              router: router
            sessionAffinity: None
            type: LoadBalancer
          ```
          {: codeblock}

    3. Create the new router service.
      ```
      oc apply -f router-new.yaml
      ```
      {: pre}

    4. Get the **EXTERNAL-IP** address of the new router service. This IP address is from a subnet on the new VLAN.
      ```
      oc get svc router-new
      ```
      {: pre}

      Example output:
      ```
      NAME                         TYPE           CLUSTER-IP       EXTERNAL-IP     PORT(S)                                     AGE
      router-new                   LoadBalancer   172.21.XX.XX     169.XX.XXX.XX   80:31049/TCP,443:30219/TCP                  2m
      ```
      {: screen}

    5. **Multizone clusters**: If you changed the VLANs for worker nodes in multiple zones, repeat these steps to create a router service on the new VLANs in each zone.

2. Note the **Hostname** of the router. In the output, look for the hostname formatted like `<cluster_name>-<random_hash>-0001.<region>.containers.appdomain.cloud`.
  ```
  ibmcloud oc nlb-dns ls -c <cluster_name_or_ID>
  ```
  {: pre}

  Example output:
  ```
  Hostname                                                                             IP(s)           Health Monitor   SSL Cert Status   SSL Cert Secret Name                            Secret Namespace
  mycluster-35366fb2d3d90fd50548180f69e7d12a-0001.us-east.containers.appdomain.cloud   169.XX.XXX.XX   None             created           roks-ga-35366fb2d3d90fd50548180f69e7d12a-0001   default
  ...
  ```
  {: screen}

3. Add the IP address of the new router service that you found in step 1 to the router's hostname. If you created services for multiple zones in step 1, include each IP address separately in repeated `--ip` flags.
  ```
  ibmcloud oc nlb-dns add -c <cluster_name_or_ID> --ip <new_IP> --nlb-host <subdomain>
  ```
  {: pre}
  Your router service on the new VLAN is now registered with the domain for the default router in your cluster, and can forward incoming requests to apps.

4. Get the IP address of the old router service on the old VLAN. **Multizone clusters**: If you changed the VLANs for worker nodes in multiple zones, get the IP address for the router service in each zone where the VLANs changed. Note that the router service in the first zone where you have workers nodes is always named `router`, and router services in the zones that you subsequently add to your cluster have names such as `router-dal12`.
    ```
    oc get svc
    ```
    {: pre}

    Example output for a multizone cluster:
    ```
    NAME                          TYPE           CLUSTER-IP       EXTERNAL-IP      PORT(S)                      AGE
    router                        LoadBalancer   172.21.47.119    169.XX.XX.XX     80:31311/TCP,443:32561/TCP   78d
    router-dal12                  LoadBalancer   172.21.190.62    169.XX.XX.XX     80:32318/TCP,443:30915/TCP   51d
    router-internal-default       ClusterIP      172.21.51.30     <none>           80/TCP,443/TCP,1936/TCP      78d
    ```
    {: screen}

5. Remove the IP address of the old router service that you found in step 2 from the router's hostname. For multizone clusters, include each IP address separately in repeated `--ip` flags.
  ```
  ibmcloud oc nlb-dns rm classic -c <cluster_name_or_ID> --ip <old_IP> --nlb-host <hostname>
  ```
  {: pre}

6. Verify that the hostname for your router is now registered with the new IP address. After your router hostname is updated with the IP address of the new service, no further changes to your router or routes are required.
  ```
  ibmcloud oc nlb-dns ls -c <cluster_name_or_ID>
  ```
  {: pre}

7. Delete the router service on the old VLAN.
    ```
    oc delete svc <old_router_svc>
    ```
    {: pre}

8. Optional: If you no longer need the subnets on the old VLANs, you can [remove them](/docs/openshift?topic=openshift-subnets#remove-subnets).


