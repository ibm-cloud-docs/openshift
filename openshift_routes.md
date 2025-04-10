---

copyright:
  years: 2014, 2025
lastupdated: "2025-04-09"


keywords: openshift, route, router

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}



# Exposing apps with routes in {{site.data.keyword.redhat_openshift_notm}} 4
{: #openshift_routes}
{: help}
{: support}

Expose the services in your {{site.data.keyword.openshiftlong}} cluster on the router's external IP address by using a route.
{: shortdesc}

This information is for clusters that run {{site.data.keyword.redhat_openshift_notm}} version 4.
{: important}

Not sure whether to use {{site.data.keyword.redhat_openshift_notm}} routes or Ingress? Check out [Choosing among load balancing solutions](/docs/openshift?topic=openshift-cs_network_planning).
{: tip}

## Overview
{: #routes-overview}

By default, a {{site.data.keyword.redhat_openshift_notm}} Ingress controller is deployed to your cluster that functions as the ingress endpoint for external network traffic.
{: shortdesc}

You can use the {{site.data.keyword.redhat_openshift_notm}} Ingress controller to create routes for your apps. Routes are assigned a publicly or privately accessible hostname from the Ingress controller subdomain that external clients can use to send requests to your app. You can choose to create unsecured or secured routes by using the TLS certificate of the Ingress controller to secure your hostname. When external request reach your hostname, the Ingress controller proxies your request and forwards it to the private IP address that your app listens on.

The type of Ingress controller that is created by default varies depending on your cluster's infrastructure provider and your service endpoint setup.
* **Classic clusters / VPC clusters with public cloud service endpoint**: Your cluster is created with a public Ingress controller by default. The Ingress controller assigns publicly accessible routes for your apps and listens for requests to your apps on the public host network interface. When a request is received, the Ingress controller directs the request to the private IP address that the app listens on. If you want to privately expose your apps instead, you must first create a private Ingress controller, and then create private routes.
* **VPC clusters with private cloud service endpoint only**: Your cluster is created with a private Ingress controller by default. The Ingress controller assigns privately accessible routes for your apps and listens on the private host network interface. Only clients that are connected to your private VPC network can access apps that are exposed by a private route. If you want to publicly expose your apps instead, you must first create a public Ingress controller, and then create public routes.

If you have a multizone cluster, one high-availability Ingress controller is deployed to your cluster, and one Ingress controller service is created in each zone. Two worker nodes are required per zone so that the two replicas of the Ingress controller can be deployed and updated correctly. Note that the Ingress controller service in the first zone where you have workers nodes is always named `router-default`, and Ingress controller services in zones that you subsequently add to your cluster have names such as `router-dal12`.
* To see the Ingress controller services in each zone of your cluster, run `oc get svc -n openshift-ingress`.
* To see the Ingress controller subdomain for your cluster and the IP addresses for the Ingress controller service in each zone, run `ibmcloud oc nlb-dns ls -c <cluster_name_or_ID>` and look for the subdomain formatted like `<cluster_name>-<random_hash>-0000.<region>.containers.appdomain.cloud`.

In your VPC infrastructure dashboard, the VPC load balancer reports as healthy only the two worker nodes that run the Ingress controller replica pods, because these worker nodes are configured as the listeners for the VPC load balancer. Even though only the listener worker nodes are reported as healthy, the listeners' backend pool of worker nodes is kept up-to-date by {{site.data.keyword.openshiftlong_notm}} so that all worker nodes in your cluster can still receive requests from the VPC load balancer.
{: note}

### Traffic flow in a classic single-zone cluster
{: #route_single}

The following diagram shows how a router directs network traffic from the internet to an app in a single-zone, classic cluster.
{: shortdesc}

![Expose an app in a single-zone {{site.data.keyword.redhat_openshift_notm}} cluster by using a router](images/roks-router.svg){: caption="Expose an app in a single-zone cluster by using a router" caption-side="bottom"}

1. A request to your app uses the route hostname that you set up for your app.

2. A DNS service resolves the subdomain to the portable public IP address of router service.

3. The router receives the request, and forwards it to the private IP address of the app pod over the private network. The source IP address of the request package is changed to the public IP address of the worker node where the router pod runs. If multiple app instances are deployed in the cluster, the router sends the requests between the app pods.

4. When the app returns a response packet, it uses the IP address of the worker node where the router that forwarded the client request exists. The router then sends the response packet through the load balancer service to the client.

### Traffic flow in a classic multizone cluster
{: #route_multi}

The following diagram shows how a router directs network traffic from the internet to an app in a multizone, classic cluster.
{: shortdesc}

![Expose an app in a multizone {{site.data.keyword.redhat_openshift_notm}} cluster by using a router](images/roks-router-multi.svg){: caption="Expose an app in a multizone cluster by using a router" caption-side="bottom"}

1. A request to your app uses the route hostname that you set up for your app.

2. A DNS service resolves the route subdomain to the portable public IP address of a router service that was reported as healthy by the multizone load balancer (MZLB). The MZLB continuously checks the portable public IP addresses of the services that expose the router in each zone in your cluster. Requests are handled by the router services in various zones in a round-robin cycle.

3. Based on the resolved IP address of the router service, the router receives the request.

4. The router forwards the request to the private IP address of the app pod over the private network. The source IP address of the request package is changed to the public IP address of the worker node where the router pod runs. Each router sends requests to the app instances in its own zone and to app instances in other zones. Additionally, if multiple app instances are deployed in one zone, the router alternates requests between app pods.

5. When the app returns a response packet, it uses the IP address of the worker node where the router that forwarded the client request exists. The router then sends the response packet through the load balancer service to the client.


### Traffic flow in a multizone VPC cluster with a public cloud service endpoint
{: #route_vpc}

When you create a multizone VPC cluster with the public cloud service endpoint enabled, a public Ingress controller is created by default. The Ingress controller assigns publicly accessible routes for your apps and listens for requests to your apps on the public host network interface.
{: shortdesc}

The following diagram shows how a Ingress controller directs network traffic from the internet to an app in a multizone, VPC cluster.

![Expose an app in a multizone VPC cluster by using an Ingress controller](images/traffic-flow-multizone-vpc-public.svg "Expose an app in a multizone VPC cluster by using an Ingress controller"){: caption="Expose an app in a multizone VPC cluster by using an Ingress controller" caption-side="bottom"}



1. A request to your app uses the route hostname that you set up for your app.

1. A DNS service resolves the route subdomain to the VPC load balancer hostname that is assigned to the services for the Ingress controller. In VPC clusters, your Ingress controller services' external IP addresses are floating, and are kept behind a VPC-assigned hostname.

1. The VPC load balancer resolves the VPC hostname to an available external IP address of a Ingress controller service that was reported as healthy. The VPC load balancer continuously checks the external IP addresses of the services that expose the Ingress controller in each zone in your cluster.

1. Based on the resolved IP address, the VPC load balancer sends the request to a Ingress controller service.

1. The Ingress controller forwards the request to the private IP address of the app pod over the private network. The source IP address of the request packet is changed to the IP address of the worker node where the Ingress controller pod runs. Each Ingress controller sends requests to the app instances in its own zone and to app instances in other zones. Additionally, if multiple app instances are deployed in one zone, the Ingress controller alternates requests between app pods.

1. When the app returns a response packet, it uses the IP address of the worker node where the Ingress controller that forwarded the client request exists. The Ingress controller then sends the response packet through the VPC load balancer to the client.

### Traffic flow in a multizone VPC cluster with a private cloud service endpoint only
{: #route_vpc_private}

When you create a multizone VPC cluster with the private cloud service endpoint only, a private Ingress controller is created by default. The Ingress controller assigns privately accessible routes for your apps and listens on the private host network interface. Only clients that are connected to your private VPC network can access apps that are exposed by a private route.
{: shortdesc}

The following diagram shows how a Ingress controller directs network traffic from private networks to an app in a multizone, VPC cluster.

![Expose an app in a private, multizone, VPC cluster by using a Ingress controller](images/traffic-flow-multizone-vpc-private.svg "Expose an app in a private, multizone, VPC cluster by using a Ingress controller"){: caption="Expose an app in a private, multizone, VPC cluster by using a Ingress controller" caption-side="bottom"}

1. A client that is connected to your private VPC network sends a request to your app by using the app's private route. For example, you might use the Virtual Private Cloud VPN, {{site.data.keyword.tg_full_notm}}, or {{site.data.keyword.dl_full_notm}} to allow requests from an on-premises network, another VPC, or {{site.data.keyword.cloud_notm}} classic infrastructure to apps that run in your cluster.

1. A DNS service resolves the route subdomain to the VPC load balancer hostname that is assigned to the services for the Ingress controller. In VPC clusters, your Ingress controller services' IP addresses are floating, and are kept behind a VPC-assigned hostname. Note that though the DNS record for the route subdomain is registered in the public DNS system, the DNS resolution servers are reachable from the VPC.

1. The private VPC load balancer resolves the VPC hostname to an available private IP address of a Ingress controller service that was reported as healthy. The VPC load balancer continuously checks the IP addresses of the services that expose the Ingress controller in each zone in your cluster.

1. Based on the resolved IP address, the VPC load balancer sends the request to a Ingress controller service.

1. The Ingress controller forwards the request to the private IP address of the app pod over the private network. The source IP address of the request packet is changed to the IP address of the worker node where the Ingress controller pod runs. Each Ingress controller sends requests to the app instances in its own zone and to app instances in other zones. Additionally, if multiple app instances are deployed in one zone, the Ingress controller alternates requests between app pods.

1. When the app returns a response packet, it uses the IP address of the worker node where the Ingress controller that forwarded the client request exists. The Ingress controller then sends the response packet through the VPC load balancer and through the {{site.data.keyword.vpc_short}} VPN, {{site.data.keyword.tg_short}}, or {{site.data.keyword.dl_short}} to the client.


## Route types and TLS termination
{: #route-types}

{{site.data.keyword.redhat_openshift_notm}} offers four types of routes based on the type of TLS termination that your app requires. Each route type is supported for public and private routes.
{: shortdesc}

| Route type | Use case |
| ---------- | -------- |
| Simple | If you don't need TLS encryption, create a simple route to handle non-encrypted HTTP traffic. |
| Passthrough | When you want TLS connections to pass uninterruptedly from the client to your app pod, create a passthrough route. The router is not involved in TLS termination for encrypted HTTPS traffic, so the app pod must terminate the TLS connection. This type can also be used for HTTP/2 and for non-HTTP TLS endpoints. |
| Edge | When your app pod is exposed on a non-encrypted HTTP endpoint, but you must handle encrypted HTTPS traffic, create an edge route. The TLS connection between the client and the router service is terminated, and the connection between the router service and your app pod is unencrypted. For more information, see the [{{site.data.keyword.redhat_openshift_notm}} edge route documentation](https://docs.openshift.com/container-platform/4.17/networking/routes/secured-routes.html#nw-ingress-creating-an-edge-route-with-a-custom-certificate_secured-routes){: external}. |
| Re-encrypt | When your app pod is exposed on an encrypted HTTPS endpoint and you must handle HTTPS traffic, create a re-encrypt route. The TLS connection between the client and the router service is terminated, and a new TLS connection between the router service and your app pod is created. For more information, see the [{{site.data.keyword.redhat_openshift_notm}} re-encrypt route documentation](https://docs.openshift.com/container-platform/4.17/networking/routes/secured-routes.html#nw-ingress-creating-a-reencrypt-route-with-a-custom-certificate_secured-routes){: external}. |
{: caption="Types of routes based on TLS termination"}

If you don't need to use a custom domain, you can use an IBM-provided route hostname in the format `<service_name>-<project>.<cluster_name>-<random_hash>-0000.<region>.containers.appdomain.cloud`.

## Ingress controller health checks
{: #health-checks}

Allow access through network policies or other firewall rules so that your Ingress controller services are reachable by the Ingress controller health check.
{: shortdesc}

**Classic**: If you use Calico pre-DNAT network policies or another custom firewall to block incoming traffic to your cluster, you must allow inbound access on port 80 from the {{site.data.keyword.redhat_openshift_notm}} control plane and Akamai's IPv4 IP addresses to the IP addresses of your Ingress controller services so that the {{site.data.keyword.redhat_openshift_notm}} control plane can check the health of your Ingress controllers. For example, if you use Calico policies, [create a Calico pre-DNAT policy](/docs/openshift?topic=openshift-network_policies#isolate_workers) to allow inbound access to your Ingress controllers from [Akamai's source IP addresses](https://github.com/IBM-Cloud/kube-samples/tree/master/akamai/gtm-liveness-test){: external} that are used to check the health of your Ingress controllers on port 80 and the [control plane subnets for the region where your cluster is located](https://github.com/IBM-Cloud/kube-samples/tree/master/control-plane-ips){: external}. Continue to the next step to get the Ingress controller service IP addresses.

**VPC**: If you set up [VPC security groups](/docs/openshift?topic=openshift-vpc-security-group) or [VPC access control lists (ACLs)](/docs/openshift?topic=openshift-vpc-acls) to secure your cluster network, ensure that you create the rules to allow the necessary traffic from the {{site.data.keyword.redhat_openshift_notm}} control plane IP addresses. Alternatively, to allow the inbound traffic for Ingress controller health checks, you can create one rule to allow all incoming traffic on port 80.

## Setting up public routes
{: #routes-setup}

Use a public Ingress controller to expose apps in your cluster.
{: shortdesc}

The method for setting up public routes varies depending on your cluster's infrastructure provider and your service endpoint setup.
* [Setting up public routes in classic clusters or in VPC clusters with a public cloud service endpoint](#routes-public-classic)
* [Setting up public routes in VPC clusters with a private cloud service endpoint only](#routes-public-vpc-privse)

### Setting up public routes in classic clusters or in VPC clusters with a public cloud service endpoint
{: #routes-public-classic}

If your cluster is created on classic infrastructure, or if your cluster is created on VPC infrastructure and you enabled the public cloud service endpoint during cluster creation, your cluster is created with a public Ingress controller by default. You can use this Ingress controller to create public routes for your app.
{: shortdesc}

1. Create a Kubernetes `ClusterIP` service for your app deployment. The service provides an internal IP address for the app that the Ingress controller can send traffic to.
    ```sh
    oc expose deploy <app_deployment_name> --name my-app-svc
    ```
    {: pre}

1. Choose a domain for your app. Note that route URLs must be 130 characters or fewer **IBM-provided domain**: If you don't need to use a custom domain, a route hostname is generated for you in the format `<service_name>-<project>.<cluster_name>-<random_hash>-0000.<region>.containers.appdomain.cloud`. **Custom domain**: To specify a custom domain, work with your DNS provider or [{{site.data.keyword.cis_full}}](https://cloud.ibm.com/catalog/services/internet-services).

    1. Get the public IP address for the public Ingress controller service in each zone in the **EXTERNAL-IP** column. Note that the Ingress controller service in the first zone where you have workers nodes is always named `router-default`, and Ingress controller services in zones that you subsequently add to your cluster have names such as `router-dal12`.
        ```sh
        oc get svc -n openshift-ingress
        ```
        {: pre}

    1. Create a custom domain with your DNS provider.
        If you want to use the same subdomain for multiple services in your cluster, you can register a wildcard subdomain, such as `*.example.com`.
        {: tip}

    1. Map your custom domain to the Ingress controller's public IP address by adding the IP address as an A record.

1. Set up a route that is based on the [type of TLS termination that your app requires](#route-types). If you don't have a custom domain, don't include the `--hostname` option. A route hostname is generated for you in the format `<service_name>-<project>.<cluster_name>-<random_hash>-0000.<region>.containers.appdomain.cloud`. If you registered a wildcard subdomain, specify a unique subdomain in each route that you create. For example, you might specify `--hostname svc1.example.com` in this route, and `--hostname svc2.example.com` in another route.
    * Simple:
        ```sh
        oc expose service <app_service_name> [--hostname <subdomain>]
        ```
        {: pre}

    * Passthrough:
        ```sh
        oc create route passthrough --service <app_service_name> [--hostname <subdomain>]
        ```
        {: pre}

        Need to handle HTTP/2 connections? After you create the route, run `oc edit route <app_service_name>` and change the route's `targetPort` value to `https`. You can test the route by running `curl -I --http2 https://<route> --insecure`.
    * Edge: If you use a custom domain, include `--hostname`, `--cert`, and `--key` options, and optionally the `--ca-cert` option. For more information about the TLS certificate requirements, see the [{{site.data.keyword.redhat_openshift_notm}} edge route documentation](https://docs.openshift.com/container-platform/4.17/networking/routes/secured-routes.html#nw-ingress-creating-an-edge-route-with-a-custom-certificate_secured-routes){: external}.
        ```sh
        oc create route edge --service <app_service_name> [--hostname <subdomain> --cert <tls.crt> --key <tls.key> --ca-cert <ca.crt>]
        ```
        {: pre}

    * Re-encrypt: If you use a custom domain, include `--hostname`, `--cert`, and `--key` options, and optionally the `--ca-cert` option. For more information about the TLS certificate requirements, see the [{{site.data.keyword.redhat_openshift_notm}} re-encrypt route documentation](https://docs.openshift.com/container-platform/4.17/networking/routes/secured-routes.html#nw-ingress-creating-a-reencrypt-route-with-a-custom-certificate_secured-routes){: external}.
        ```sh
        oc create route reencrypt --service <app_service_name> --dest-ca-cert <destca.crt> [--hostname <subdomain> --cert <tls.crt> --key <tls.key> --ca-cert <ca.crt>]
        ```
        {: pre}

1. Verify that the route for your app service is created.
    ```sh
    oc get routes
    ```
    {: pre}

1. Optional: Customize default routing rules with [optional configurations](https://docs.openshift.com/container-platform/4.17/networking/routes/route-configuration.html){: external}. For example, you can use [route-specific HAProxy annotations](https://docs.openshift.com/container-platform/4.17/networking/routes/route-configuration.html#nw-route-specific-annotations_route-configuration){: external}.

### Setting up public routes in VPC clusters with a private cloud service endpoint only
{: #routes-public-vpc-privse}

If your cluster is created on VPC infrastructure and you enabled only the private cloud service endpoint during cluster creation, your cluster is created with only a private router by default. To publicly expose your apps, you must first create a public IngressController resource and configure that with a subdomain. The Ingress operator automatically creates and configures a new public Ingress controller based on the IngressController, which you can use to create public routes for your apps.
{: shortdesc}

Note that even though you create an IngressController resource in the following steps, the IngressController is only required to create and configure the necessary Ingress controller for you. After the Ingress controller is created, you use the Ingress controller directly to create routes.

1. Prepare the domain that you want to use for your Ingress controller.
    * **Custom domain**: To register a custom domain, work with your Domain Name Service (DNS) provider or [{{site.data.keyword.cloud_notm}} DNS](/docs/dns-svcs?topic=dns-svcs-getting-started). If you want to use the same subdomain for multiple services in your cluster, you can register a wildcard subdomain, such as `*.example.com`. If you use a custom domain, you must also specify the domain certificate in your `IngressController` specification. For more information, see [Setting a custom default certificate](https://docs.redhat.com/documentation/openshift_container_platform/4.11/html/networking/configuring-ingress#nw-ingress-controller-configuration-parameters_configuring-ingress){: external}
    * **IBM-provided domain**:
        1. List the existing subdomains in your cluster. In the **Subdomain** column of the output, copy the subdomain that has the highest `000<n>` value.
            ```sh
            ibmcloud oc nlb-dns ls --cluster <cluster_name_or_id>
            ```
            {: pre}

            In this example output, the `mycluster-a1b2cdef345678g9hi012j3kl4567890-0002.us-south.containers.appdomain.cloud` subdomain has the highest `000<n>` value of `0002`.
            ```sh
            Subdomain                                                                               Load Balancer Hostname                        Health Monitor   SSL Cert Status           SSL Cert Secret Name
            mycluster-a1b2cdef345678g9hi012j3kl4567890-0000.us-south.containers.appdomain.cloud     ["1234abcd-us-south.lb.appdomain.cloud"]      None             created                   mycluster-a1b2cdef345678g9hi012j3kl4567890-0000
            mycluster-a1b2cdef345678g9hi012j3kl4567890-0001.us-south.containers.appdomain.cloud     ["5678efgh-us-south.lb.appdomain.cloud"]      None             created                   mycluster-a1b2cdef345678g9hi012j3kl4567890-0001
            mycluster-a1b2cdef345678g9hi012j3kl4567890-0002.us-south.containers.appdomain.cloud     ["9012ijkl-us-south.lb.appdomain.cloud"]      None             created                   mycluster-a1b2cdef345678g9hi012j3kl4567890-0002
            ```
            {: screen}

        1. In the subdomain that you copied, change the `000<n>` value in the subdomain to `000<n+1>`. For example, the `mycluster-a1b2cdef345678g9hi012j3kl4567890-0002.us-south.containers.appdomain.cloud` subdomain is changed to `mycluster-a1b2cdef345678g9hi012j3kl4567890-0003.us-south.containers.appdomain.cloud`. You register this subdomain  in later steps.

1. Create a YAML file that configures a public Ingress controller with the domain from step 1.
    ```yaml
    apiVersion: operator.openshift.io/v1
    kind: IngressController
    metadata:
      name: public
      namespace: openshift-ingress-operator
    spec:
      # defaultCertificate: If you are using a custom domain, specify the domain certificate
        # name: custom-certs-default
      replicas: 2
      domain: <domain>
      endpointPublishingStrategy:
        loadBalancer:
          scope: External
        type: LoadBalancerService
    ```
    {: codeblock}

1. Create the IngressController resource in the `openshift-ingress-operator` namespace of your cluster. When you create the IngressController, a public Ingress controller is automatically created and deployed in the `openshift-ingress` namespace based on the IngressController settings. Additionally, a Ingress controller service is created to expose the Ingress controller.
    ```sh
    oc create -f public.yaml -n openshift-ingress-operator
    ```
    {: pre}

1. Get the VPC hostname in the **EXTERNAL IP** field of the `router-public` service. In VPC clusters, your router services' external IP addresses are floating, and are instead kept behind a VPC-assigned hostname.
    ```sh
    oc get svc router-public -n openshift-ingress
    ```
    {: pre}

    Example output

    ```sh
    NAME                         TYPE           CLUSTER-IP       EXTERNAL-IP                             PORT(S)                      AGE
    router-public                LoadBalancer   172.21.57.132    1234abcd-us-south.lb.appdomain.cloud    80/TCP,443/TCP,1940/TCP      3m
    ```
    {: screen}

1. Register the service's VPC hostname with the domain that you chose in step 1. This step ensures that your Ingress controller services' IP addresses, which are kept behind the VPC hostname, are registered with the domain that you chose for the Ingress controller.
    * **Custom domain**: Work with your DNS provider to add the service's VPC hostname as a CNAME that maps to your custom domain.
    * **IBM-provided domain**: Create a DNS entry for the service's VPC hostname. When you run the following command, the subdomain that you specified in step 2 is automatically generated, and is registered with the Ingress controller service.
    
        ```sh
        ibmcloud oc nlb-dns create vpc-gen2 --cluster <cluster_name_or_ID> --lb-host <router_VPC_hostname>
        ```
        {: pre}

1. **Optional**: If you want to use Ingress controller sharding so that specific routes are handled by a specific Ingress controller, for example private routes be admitted only to a private router, then you can use either route labels or namespace labels to specify the sharding method. To add the selector during creation time, include it in the `ingresscontroller` yaml under `spec`. For example, to allow an Ingress controller to only handle ingress/routes with label `type=sharded`, you can add a `routeSelector`. For more information, see [Ingress controller sharding](https://docs.redhat.com/documentation/openshift_container_platform/4.8/html/networking/configuring-ingress#nw-ingress-sharding_configuring-ingress){: external}.
    ```yaml
      routeSelector:
        matchLabels:
          type: sharded
    ```
    {: pre}
    
    1. To add selectors to an existing Ingress controller, get a list of Ingress controllers.
        ```sh
        oc get ingresscontroller -n openshift-ingress-operator
        ```
        {: pre}
        
    1. Add the selectors to Ingress controllers where you want to use sharding.
        
        ```sh
        oc patch  -n openshift-ingress-operator IngressController/<name>   --type='merge'   -p '{"spec":{"routeSelector":{"matchLabels":{"type":"sharded"}}}}'
        ```
        {: pre}


    1. Note that no selectors are added to the default IngressController, so all routes are still admitted to the default Ingress controller on the cluster. You can use the relevant route or a namespace label selectors to change this behavior. For example, to adjust default router to skip ingress/routes with label `type=sharded`, run the following patch command.
        ```sh
        oc patch -n openshift-ingress-operator IngressController/default --type='merge'   -p '{"spec":{"routeSelector":{"matchExpressions":[{"key":"type","operator":"NotIn","values":["sharded"]}]}}}'
        ```
        {: pre}

        Several routes and Ingresses on the cluster depend on the default public ingress controller. Make sure the changes are desired before editing the default Ingress controller. For more information about, see [Ingress controller sharding](https://docs.redhat.com/documentation/openshift_container_platform/4.8/html/networking/configuring-ingress#nw-ingress-sharding_configuring-ingress){: external}.
        {: note}
    

1. Create a Kubernetes `ClusterIP` service for your app deployment. The service provides an internal IP address for the app that the Ingress controller can send traffic to.
    ```sh
    oc expose deploy <app_deployment_name> --name <app_service_name> -n <app_project>
    ```
    {: pre}

1. Set up a route that is based on the [type of TLS termination that your app requires](#route-types). If you don't include the `--hostname` option, the route hostname is generated for you in the format `<app_service_name>-<app_project>.<router-subdomain>`.
    * Simple:
        ```sh
        oc expose service <app_service_name> [--hostname <subdomain>]
        ```
        {: pre}

    * Passthrough:
        ```sh
        oc create route passthrough --service <app_service_name> [--hostname <subdomain>]
        ```
        {: pre}

        Need to handle HTTP/2 connections? After you create the route, run `oc edit route <app_service_name>` and change the route's `targetPort` value to `https`. You can test the route by running `curl -I --http2 https://<route> --insecure`.
    * Edge: If you use a custom domain, include `--hostname`, `--cert`, and `--key` options, and optionally the `--ca-cert` option. For more information about the TLS certificate requirements, see the [{{site.data.keyword.redhat_openshift_notm}} edge route documentation](https://docs.openshift.com/container-platform/4.17/networking/routes/secured-routes.html#nw-ingress-creating-an-edge-route-with-a-custom-certificate_secured-routes){: external}.
        ```sh
        oc create route edge --service <app_service_name> [--hostname <subdomain> --cert <tls.crt> --key <tls.key> --ca-cert <ca.crt>]
        ```
        {: pre}

    * Re-encrypt: If you use a custom domain, include `--hostname`, `--cert`, and `--key` options, and optionally the `--ca-cert` option. For more information about the TLS certificate requirements, see the [{{site.data.keyword.redhat_openshift_notm}} re-encrypt route documentation](https://docs.openshift.com/container-platform/4.17/networking/routes/secured-routes.html#nw-ingress-creating-a-reencrypt-route-with-a-custom-certificate_secured-routes){: external}.
        ```sh
        oc create route reencrypt --service <app_service_name> --dest-ca-cert <destca.crt> [--hostname <subdomain> --cert <tls.crt> --key <tls.key> --ca-cert <ca.crt>]
        ```
        {: pre}

1. Verify that the route for your app is created.
    ```sh
    oc get routes
    ```
    {: pre}

1. Optional: Customize the public Ingress controller's routing rules with [optional configurations](https://docs.openshift.com/container-platform/4.17/networking/routes/route-configuration.html){: external}. For example, you can use [route-specific HAProxy annotations](https://docs.openshift.com/container-platform/4.17/networking/routes/route-configuration.html#nw-route-specific-annotations_route-configuration){: external}.

1. To create routes for more apps by using the same subdomain, you can repeat steps 7 - 10 so that the route is generated by the same public Ingress controller. If you want to create routes for more apps by using a different subdomain, repeat all steps in this section to create a new public Ingress controller with a different domain.



## Setting up private routes
{: #private-routes}

Use a private Ingress controller to expose apps in your cluster on the private network.
{: shortdesc}

The method for setting up private routes varies depending on your cluster's infrastructure provider and your service endpoint setup.
* [Setting up private routes in classic clusters or in VPC clusters with a public cloud service endpoint](#private-routes-setup-43)
* [Setting up private routes in VPC clusters with a private cloud service endpoint only](#routes-private-vpc-privse)

### Setting up private routes in classic clusters or in VPC clusters with a public cloud service endpoint
{: #private-routes-setup-43}

If your cluster is created on classic infrastructure, or if your cluster is created on VPC infrastructure and you enabled the public cloud service endpoint during cluster creation, your cluster is created with only a public Ingress controller by default. To privately expose your apps, you must first create a private IngressController resource and configure the controller with a subdomain. The Ingress operator automatically creates and configures a new private Ingress controller, which you can use to create private routes for your apps.
{: shortdesc}

Note that even though you create an IngressController resource in the following steps, the IngressController resource is only required to create and configure the necessary Ingress controller for you. After the Ingress controller is created, you use the router directly to create routes.

1. Prepare the domain that you want to use for your Ingress controller.
    * **Custom domain, classic or VPC clusters**: To register a custom domain, work with your Domain Name Service (DNS) provider or [{{site.data.keyword.cloud_notm}} DNS](/docs/dns-svcs?topic=dns-svcs-getting-started). If you want to use the same subdomain for multiple services in your cluster, you can register a wildcard subdomain, such as `*.example.com`.
    * **IBM-provided domain, VPC clusters only**:
        1. List the existing subdomains in your cluster. In the **Subdomain** column of the output, copy the subdomain that has the highest `000<n>` value.
            ```sh
            ibmcloud oc nlb-dns ls --cluster <cluster_name_or_id>
            ```
            {: pre}

            In this example output, the `mycluster-a1b2cdef345678g9hi012j3kl4567890-0002.us-south.containers.appdomain.cloud` subdomain has the highest `000<n>` value of `0002`.
            ```sh
            Subdomain                                                                               Load Balancer Hostname                        Health Monitor   SSL Cert Status           SSL Cert Secret Name
            mycluster-a1b2cdef345678g9hi012j3kl4567890-0000.us-south.containers.appdomain.cloud     ["1234abcd-us-south.lb.appdomain.cloud"]      None             created                   mycluster-a1b2cdef345678g9hi012j3kl4567890-0000
            mycluster-a1b2cdef345678g9hi012j3kl4567890-0001.us-south.containers.appdomain.cloud     ["5678efgh-us-south.lb.appdomain.cloud"]      None             created                   mycluster-a1b2cdef345678g9hi012j3kl4567890-0001
            mycluster-a1b2cdef345678g9hi012j3kl4567890-0002.us-south.containers.appdomain.cloud     ["9012ijkl-us-south.lb.appdomain.cloud"]      None             created                   mycluster-a1b2cdef345678g9hi012j3kl4567890-0002
            ```
            {: screen}

        1. In the subdomain that you copied, change the `000<n>` value in the subdomain to `000<n+1>`. For example, the `mycluster-a1b2cdef345678g9hi012j3kl4567890-0002.us-south.containers.appdomain.cloud` subdomain is changed to `mycluster-a1b2cdef345678g9hi012j3kl4567890-0003.us-south.containers.appdomain.cloud`. You register this subdomain  in later steps.

1. Create a configuration file that configures a private Ingress controller with the domain from step 1.
    ```yaml
    apiVersion: operator.openshift.io/v1
    kind: IngressController
    metadata:
      name: private
      namespace: openshift-ingress-operator
    spec:
      replicas: 2
      domain: <domain>
      endpointPublishingStrategy:
        loadBalancer:
          scope: Internal
        type: LoadBalancerService
    ```
    {: codeblock}

1. Create the IngressController resource in the `openshift-ingress-operator` namespace of your cluster. When you create the IngressController resource, a private Ingress controller is automatically created and deployed in the `openshift-ingress` namespace based on the IngressController settings. Additionally, a Ingress controller service is created to expose the Ingress controller with an IP address (classic clusters) or a VPC hostname (VPC clusters).
    ```sh
    oc create -f private.yaml -n openshift-ingress-operator
    ```
    {: pre}

1. Get the IP address or VPC hostname in the **EXTERNAL IP** field of the `router-private` service.
    ```sh
    oc get svc router-private -n openshift-ingress
    ```
    {: pre}

    Example output for classic clusters:
    ```sh
    NAME                         TYPE           CLUSTER-IP       EXTERNAL-IP    PORT(S)                      AGE
    router-private               LoadBalancer   172.21.57.132    10.XX.XX.XX    80/TCP,443/TCP,1940/TCP      3m
    ```
    {: screen}

    Example output for VPC clusters:
    ```sh
    NAME                         TYPE           CLUSTER-IP       EXTERNAL-IP                             PORT(S)                      AGE
    router-private               LoadBalancer   172.21.57.132    1234abcd-us-south.lb.appdomain.cloud    80/TCP,443/TCP,1940/TCP      3m
    ```
    {: screen}

1. Register the service's external IP address or VPC hostname with the domain that you chose in step 1.
    * **Custom domain, classic or VPC clusters**: Work with your DNS provider to add the service's external IP address as an A record (classic clusters) or VPC hostname as a CNAME (VPC clusters) that maps to your custom domain.
    * **IBM-provided domain, VPC clusters only**: Create a DNS entry for the service's VPC hostname. When you run the following command, the subdomain that you specified in step 2 is automatically generated, and is registered with the Ingress controller service.
        ```sh
        ibmcloud oc nlb-dns create vpc-gen2 --cluster <cluster_name_or_ID> --lb-host <router_VPC_hostname>
        ```
        {: pre}

1. **Optional**: If you want to use Ingress controller sharding so that specific routes are handled by a specific Ingress controller, for example private routes be admitted only to a private router, then you can use either route labels or namespace labels to specify the sharding method. To add the selector during creation time, include it in the `ingresscontroller` yaml under `spec`. For example, to allow an Ingress controller to only handle ingress/routes with label `type=sharded`, you can add a `routeSelector`. For more information, see [Ingress controller sharding](https://docs.redhat.com/documentation/openshift_container_platform/4.8/html/networking/configuring-ingress#nw-ingress-sharding_configuring-ingress){: external}.
    ```yaml
      routeSelector:
        matchLabels:
          type: sharded
    ```
    {: pre}
    
    1. To add selectors to an existing Ingress controller, get a list of Ingress controllers.
        ```sh
        oc get ingresscontroller -n openshift-ingress-operator
        ```
        {: pre}
        
    1. Add the selectors to Ingress controllers where you want to use sharding.
        
        ```sh
        oc patch  -n openshift-ingress-operator IngressController/<name>   --type='merge'   -p '{"spec":{"routeSelector":{"matchLabels":{"type":"sharded"}}}}'
        ```
        {: pre}


    1. Note that no selectors are added to the default IngressController, so all routes are still admitted to the default Ingress controller on the cluster. You can use the relevant route or a namespace label selectors to change this behavior. For example, to adjust default router to skip ingress/routes with label `type=sharded`, run the following patch command.
        ```sh
        oc patch -n openshift-ingress-operator IngressController/default --type='merge'   -p '{"spec":{"routeSelector":{"matchExpressions":[{"key":"type","operator":"NotIn","values":["sharded"]}]}}}'
        ```
        {: pre}

1. Create a Kubernetes `ClusterIP` service for your app deployment. The service provides an internal IP address for the app that the Ingress controller can send traffic to.
    ```sh
    oc expose deploy <app_deployment_name> --name <app_service_name> -n <app_project>
    ```
    {: pre}

1. Set up a route that is based on the [type of TLS termination that your app requires](#route-types). Specify the hostname that you set up in step 5.
    * Simple:
        ```sh
        oc expose service <app_service_name> --hostname <subdomain>
        ```
        {: pre}

    * Passthrough:
        ```sh
        oc create route passthrough --service <app_service_name> --hostname <subdomain>
        ```
        {: pre}

        Need to handle HTTP/2 connections? After you create the route, run `oc edit route <app_service_name>` and change the route's `targetPort` value to `https`. You can test the route by running `curl -I --http2 https://<route> --insecure`.
    * Edge: If you use a custom domain, include the `--cert` and `--key` options, and optionally the `--ca-cert` option. For more information about the TLS certificate requirements, see the [{{site.data.keyword.redhat_openshift_notm}} edge route documentation](https://docs.openshift.com/container-platform/4.17/networking/routes/secured-routes.html#nw-ingress-creating-an-edge-route-with-a-custom-certificate_secured-routes){: external}.
        ```sh
        oc create route edge --service <app_service_name> --hostname <subdomain> [--cert <tls.crt> --key <tls.key> --ca-cert <ca.crt>]
        ```
        {: pre}

    * Re-encrypt: If you use a custom domain, include the `--cert` and `--key` options, and optionally the `--ca-cert` option. For more information about the TLS certificate requirements, see the [{{site.data.keyword.redhat_openshift_notm}} re-encrypt route documentation](https://docs.openshift.com/container-platform/4.17/networking/routes/secured-routes.html#nw-ingress-creating-a-reencrypt-route-with-a-custom-certificate_secured-routes){: external}.
        ```sh
        oc create route reencrypt --service <app_service_name> --dest-ca-cert <destca.crt> --hostname <subdomain> [--cert <tls.crt> --key <tls.key> --ca-cert <ca.crt>]
        ```
        {: pre}

1. Verify that the route for your app is created.
    ```sh
    oc get routes
    ```
    {: pre}

1. Optional: Customize the private Ingress controller's routing rules with [optional configurations](https://docs.openshift.com/container-platform/4.17/networking/routes/route-configuration.html){: external}. For example, you can use [route-specific HAProxy annotations](https://docs.openshift.com/container-platform/4.17/networking/routes/route-configuration.html#nw-route-specific-annotations_route-configuration){: external}.

1. To create routes for more apps by using the same subdomain, you can repeat steps 7 - 10 so that the route is generated by the same private Ingress controller. If you want to create routes for more apps by using a different subdomain, repeat all steps in this section to create a new private Ingress controller.


### Setting up private routes in VPC clusters with a private cloud service endpoint only
{: #routes-private-vpc-privse}

If your cluster is created on VPC infrastructure and you enabled the only private cloud service endpoint during cluster creation, your cluster is created with a private Ingress controller by default. You can use this Ingress controller to create private routes for your app.
{: shortdesc}

1. Create a Kubernetes `ClusterIP` service for your app deployment. The service provides an internal IP address for the app that the Ingress controller can send traffic to.
    ```sh
    oc expose deploy <app_deployment_name> --name my-app-svc
    ```
    {: pre}

1. Choose a domain for your app.
    * **IBM-provided domain**: If you don't need a custom domain, a route subdomain is generated for you in the format `<service_name>-<project>.<cluster_name>-<random_hash>-0000.<region>.containers.appdomain.cloud`.
    * **Custom domain**: To specify a custom domain, work with your DNS provider or [{{site.data.keyword.cis_full}}](https://cloud.ibm.com/catalog/services/internet-services).
        1. Get the external IP address for the private Ingress controller service in each zone in the **EXTERNAL-IP** column. Note that the Ingress controller service in the first zone where you have workers nodes is always named `router-default`, and Ingress controller services in zones that you subsequently add to your cluster have names such as `router-dal12`.
            ```sh
            oc get svc -n openshift-ingress
            ```
            {: pre}

        1. Create a custom domain with your DNS provider.
            If you want to use the same subdomain for multiple services in your cluster, you can register a wildcard subdomain, such as `*.example.com`.
            {: tip}

        1. Map your custom domain to the Ingress controller services' private IP address by adding the IP addresses as A records.

1. Set up a route based on the [type of TLS termination that your app requires](#route-types). If you don't have a custom domain, don't include the `--hostname` option. A route subdomain is generated for you in the format `<service_name>-<project>.<cluster_name>-<random_hash>-0000.<region>.containers.appdomain.cloud`. If you registered a wildcard subdomain, specify a unique subdomain in each route that you create. For example, you might specify `--hostname svc1.example.com` in this route, and `--hostname svc2.example.com` in another route.
    * Simple:
        ```sh
        oc expose service <app_service_name> [--hostname <subdomain>]
        ```
        {: pre}

    * Passthrough:
        ```sh
        oc create route passthrough --service <app_service_name> [--hostname <subdomain>]
        ```
        {: pre}

        Need to handle HTTP/2 connections? After you create the route, run `oc edit route <app_service_name>` and change the route's `targetPort` value to `https`. You can test the route by running `curl -I --http2 https://<route> --insecure`.
        
    * Edge: If you use a custom domain, include `--hostname`, `--cert`, and `--key` options, and optionally the `--ca-cert` option. For more information about the TLS certificate requirements, see the [{{site.data.keyword.redhat_openshift_notm}} edge route documentation](https://docs.openshift.com/container-platform/4.17/networking/routes/secured-routes.html#nw-ingress-creating-an-edge-route-with-a-custom-certificate_secured-routes){: external}.
        ```sh
        oc create route edge --service <app_service_name> [--hostname <subdomain> --cert <tls.crt> --key <tls.key> --ca-cert <ca.crt>]
        ```
        {: pre}

    * Re-encrypt: If you use a custom domain, include `--hostname`, `--cert`, and `--key` options, and optionally the `--ca-cert` option. For more information about the TLS certificate requirements, see the [{{site.data.keyword.redhat_openshift_notm}} re-encrypt route documentation](https://docs.openshift.com/container-platform/4.17/networking/routes/secured-routes.html#nw-ingress-creating-a-reencrypt-route-with-a-custom-certificate_secured-routes){: external}.
        ```sh
        oc create route reencrypt --service <app_service_name> --dest-ca-cert <destca.crt> [--hostname <subdomain> --cert <tls.crt> --key <tls.key> --ca-cert <ca.crt>]
        ```
        {: pre}

1. Verify that the route for your app service is created.
    ```sh
    oc get routes
    ```
    {: pre}

1. Optional: Customize default routing rules with [optional configurations](https://docs.openshift.com/container-platform/4.17/networking/routes/route-configuration.html){: external}. For example, you can use [route-specific HAProxy annotations](https://docs.openshift.com/container-platform/4.17/networking/routes/route-configuration.html#nw-route-specific-annotations_route-configuration){: external}.



## Moving Ingress controller services across VLANs in classic clusters
{: #migrate-router-vlan-classic}

When you change your worker node VLAN connections, the worker nodes are connected to the new VLAN and assigned new public or private IP addresses. However, Ingress controller services can't automatically migrate to the new VLAN because they are assigned a stable, portable public or private IP address from a subnet that belongs to the old VLAN. When your worker nodes and Ingress controllers are connected to different VLANs, the Ingress controllers can't forward incoming network traffic to app pods on your worker nodes. To move your Ingress controller services to a different VLAN, you must create the Ingress controller service on the new VLAN and delete the Ingress controller service on the old VLAN.
{: shortdesc}

1. Create a Ingress controller service on the new VLAN.
    1. Create a YAML configuration file for a new Ingress controller service. Specify the zone that the Ingress controller service deploys to. Save the file as `router-new-<zone>.yaml`.
        * Public Ingress controller service:
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

        * Private Ingress controller service:
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

    1. Create the new Ingress controller service.
        ```sh
        oc apply -f router-new-<zone>.yaml -n openshift-ingress
        ```
        {: pre}

    1. Get the **EXTERNAL-IP** address of the new Ingress controller service. This IP address is from a subnet on the new VLAN.
        ```sh
        oc get svc router-new -n openshift-ingress
        ```
        {: pre}

        Example output for a public Ingress controller service:
        ```sh
        NAME                         TYPE           CLUSTER-IP       EXTERNAL-IP     PORT(S)                                     AGE
        router-new                   LoadBalancer   172.21.XX.XX     169.XX.XXX.XX   80:31049/TCP,443:30219/TCP                  2m
        ```
        {: screen}

    1. **Multizone clusters**: If you changed the VLANs for worker nodes in multiple zones, repeat these steps to create a Ingress controller service on the new VLANs in each zone.

1. Note the **Hostname** of the Ingress controller. In the output, look for the hostname formatted like `<cluster_name>-<random_hash>-0001.<region>.containers.appdomain.cloud`.
    ```sh
    ibmcloud oc nlb-dns ls -c <cluster_name_or_ID>
    ```
    {: pre}

    Example output
    
    ```sh
    Hostname                                                                             IP(s)           Health Monitor   SSL Cert Status   SSL Cert Secret Name                            Secret Namespace
    mycluster-35366fb2d3d90fd50548180f69e7d12a-0001.us-east.containers.appdomain.cloud   169.XX.XXX.XX   None             created           roks-ga-35366fb2d3d90fd50548180f69e7d12a-0001   default
    ...
    ```
    {: screen}

1. Add the IP address of the new Ingress controller service that you found in step 1 to the Ingress controller's hostname. If you created services for multiple zones in step 1, include each IP address separately in repeated `--ip` options.
    ```sh
    ibmcloud oc nlb-dns add -c <cluster_name_or_ID> --ip <new_IP> --nlb-host <subdomain>
    ```
    {: pre}

    Your Ingress controller service on the new VLAN is now registered with the domain for the default Ingress controller in your cluster, and can forward incoming requests to apps.

1. Get the IP address of the old Ingress controller service on the old VLAN. **Multizone clusters**: If you changed the VLANs for worker nodes in multiple zones, get the IP address for the Ingress controller service in each zone where the VLANs changed. Note that the Ingress controller service in the first zone where you have workers nodes is always named `router-default`, and Ingress controller services in the zones that you subsequently add to your cluster have names such as `router-dal12`.
    ```sh
    oc get svc -n openshift-ingress
    ```
    {: pre}

    Example output for a multizone cluster:
    ```sh
    NAME                          TYPE           CLUSTER-IP       EXTERNAL-IP      PORT(S)                      AGE
    router-dal12                  LoadBalancer   172.21.190.62    169.XX.XX.XX     80:32318/TCP,443:30915/TCP   51d
    router-default                LoadBalancer   172.21.47.119    169.XX.XX.XX     80:31311/TCP,443:32561/TCP   78d
    router-internal-default       ClusterIP      172.21.51.30     <none>           80/TCP,443/TCP,1936/TCP      78d
    ```
    {: screen}

1. Remove the IP address of the old Ingress controller service that you found in step 2 from the Ingress controller's hostname. **Multizone clusters**: Include each IP address separately in repeated `--ip` options.
    ```sh
    ibmcloud oc nlb-dns rm classic -c <cluster_name_or_ID> --ip <old_IP> --nlb-host <hostname>
    ```
    {: pre}

1. Verify that the hostname for your Ingress controller is now registered with the new IP address. After your Ingress controller hostname is updated with the IP address of the new service, no further changes to your Ingress controller or routes are required.
    ```sh
    ibmcloud oc nlb-dns ls -c <cluster_name_or_ID>
    ```
    {: pre}

1. Delete the Ingress controller service on the old VLAN.
    ```sh
    oc delete svc <old_router_svc> -n openshift-ingress
    ```
    {: pre}

1. Optional: If you no longer need the subnets on the old VLANs, you can [remove them](/docs/openshift?topic=openshift-subnets#remove-subnets).
