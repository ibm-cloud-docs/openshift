---

copyright:
  years: 2014, 2021
lastupdated: "2021-11-22"

keywords: openshift, route, router

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}

# Exposing apps in {{site.data.keyword.satelliteshort}} clusters
{: #sat-expose-apps}

Securely expose apps that run in your {{site.data.keyword.satelliteshort}} cluster to traffic requests from the public network, from resources that are connected to your hosts' private network, or from resources in {{site.data.keyword.cloud_notm}}.
{: shortdesc}

You have several options for exposing apps in {{site.data.keyword.satelliteshort}} clusters:
* [{{site.data.keyword.openshiftshort}} routes](#sat-expose-routes): Quickly expose apps to requests from the public or a private network with a hostname. The {{site.data.keyword.openshiftshort}} router provides DNS registration and optional certificates for your routes.
* [Third-party load balancer and {{site.data.keyword.openshiftshort}} routes](#sat-expose-byolb): Expose apps with a hostname, and add health checking for the host IP addresses that are registered in the router's DNS records.
* [NodePorts](#sat-expose-np): Expose non-HTTP(S) apps, such as UDP or TCP apps, with a NodePort in the 30000 - 32767 range.
* [{{site.data.keyword.openshiftshort}} routes and {{site.data.keyword.satelliteshort}} Link endpoints](#sat-expose-cloud): Expose your app with a private route, and create a Link endpoint of type `location` for the route. Only a resource that is connected to the {{site.data.keyword.cloud_notm}} private network can access your app.

## Exposing apps with {{site.data.keyword.openshiftshort}} routes
{: #sat-expose-routes}

Quickly expose the services in your cluster on the {{site.data.keyword.openshiftshort}} router's external IP address by using a route.
{: shortdesc}

An [{{site.data.keyword.openshiftshort}} route](/docs/openshift?topic=openshift-openshift_routes) exposes a service as a hostname in the format `<service_name>-<project>.<cluster_name>-<random_hash>-0000.upi.containers.appdomain.cloud`. A router is deployed by default to your cluster, which enables routes to be used by external clients. The router uses the service selector to find the service and the endpoints that back the service. You can configure the service selector to direct traffic through one route to multiple services. You can also create either unsecured or secured routes by using the TLS certificate that is assigned by the router for your hostname. Note that the router supports only the HTTP and HTTPS protocols.

Before you begin with routes, review the following considerations.
* **Host network connectivity**: If the hosts for your cluster have public network connectivity, your cluster is created with a public router by default. You can use this router to create public routes for your app. If the hosts for your cluster have private network connectivity only, your cluster is created with a private router by default. You can use this router to create private routes for your app that are accessible only from within your hosts' private network. To set up public routes in clusters that have private network connectivity only, first [set up your own third-party load balancer](#sat-expose-byolb) that has public network connectivity in front of your private router before completing the following steps.
* **Health checks**: DNS registration management is provided by default for your cluster's router. For example, if you remove a host that was assigned to your cluster from your location and replace it with a different host, IBM updates the host IP addresses in your router's DNS record for you. Note that while the DNS registration for routes are provided for you, no load balancer services are deployed in front of the router in your cluster. To health check the IP addresses of the hosts that are registered in the router's DNS records, you can [set up your own third-party load balancer](#sat-expose-byolb) in front of your router before completing the following steps.

To create routes for your apps:

1. Create a Kubernetes `ClusterIP` service for your app deployment. The service provides an internal IP address for the app that the router can send traffic to.
    ```sh
    oc expose deploy <app_deployment_name> --name my-app-svc
    ```
    {: pre}

2. Set up a domain for your app.
    * **IBM-provided domain**: If you don't need to use a custom domain, a route hostname is generated for you in the format `<service_name>-<project>.<cluster_name>-<random_hash>-0000.upi.containers.appdomain.cloud`. Continue to the next step.
    * **Custom domain**: Work with your DNS provider to create a custom domain. Note that if you previously set up a third-party load balancer in front of your router, work with your DNS provider to create a custom domain for the load balancer instead.
3. Get the IP addresses for the router service in the **EXTERNAL-IP** column.
    ```sh
    oc get svc router-external-default -n openshift-ingress
    ```
    {: pre}

4. Create a custom domain with your DNS provider. If you want to use the same subdomain for multiple services in your cluster, you can register a wildcard subdomain, such as `*.example.com`.


5. Map your custom domain to the router's IP addresses by adding the IP addresses as A records.

6. Set up a route that is based on the [type of TLS termination that your app requires](/docs/openshift?topic=openshift-openshift_routes#route-types). If you don't have a custom domain, don't include the `--hostname` flag so that a route hostname is generated for you. If you registered a wildcard subdomain, specify a unique subdomain in each route that you create. For example, you might specify `--hostname svc1.example.com` in this route, and `--hostname svc2.example.com` in another route.
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
        {: tip}
        
    * Edge: If you use a custom domain, include `--hostname`, `--cert`, and `--key` flags, and optionally the `--ca-cert` flag. For more information about the TLS certificate requirements, see the [{{site.data.keyword.openshiftshort}} edge route documentation](https://docs.openshift.com/container-platform/4.7/networking/routes/secured-routes.html#nw-ingress-creating-an-edge-route-with-a-custom-certificate_secured-routes){: external}.
        ```sh
        oc create route edge --service <app_service_name> [--hostname <subdomain> --cert <tls.crt> --key <tls.key> --ca-cert <ca.crt>]
        ```
        {: pre}

    * Re-encrypt: If you use a custom domain, include `--hostname`, `--cert`, and `--key` flags, and optionally the `--ca-cert` flag. For more information about the TLS certificate requirements, see the [{{site.data.keyword.openshiftshort}} re-encrypt route documentation](https://docs.openshift.com/container-platform/4.7/networking/routes/secured-routes.html#nw-ingress-creating-a-reencrypt-route-with-a-custom-certificate_secured-routes){: external}.
        ```sh
        oc create route reencrypt --service <app_service_name> --dest-ca-cert <destca.crt> [--hostname <subdomain> --cert <tls.crt> --key <tls.key> --ca-cert <ca.crt>]
        ```
        {: pre}

7. Verify that the route for your app service is created.
    ```sh
    oc get routes
    ```
    {: pre}

8. Optional: Customize default routing rules with [optional configurations](https://docs.openshift.com/container-platform/4.7/networking/routes/route-configuration.html){: external}. For example, you can use [route-specific HAProxy annotations](https://docs.openshift.com/container-platform/4.7/networking/routes/route-configuration.html#nw-route-specific-annotations_route-configuration){: external}.



## Setting up a third-party load balancer in front of the {{site.data.keyword.openshiftshort}} router
{: #sat-expose-byolb}

To health check the IP addresses of the hosts that are registered in the router's DNS records, you can set up your own third-party load balancer in front of the IP addresses for the hosts that are assigned as worker nodes to you cluster.
{: shortdesc}

For example, if you remove a host that was assigned to your cluster from your location and replace it with a different host, IBM updates the host IP addresses in your router's DNS record for you. But if you power off a host, such as through your cloud provider's infrastructure management, the host's IP address is not removed from your router's DNS records and might cause a call to fail if the DNS record is resolved to that host's IP address. By setting up a load balancer in front of your router, you can ensure that host IP addresses are regularly health checked, such as to ensure high availability for production-level workloads.

After you create a load balancer in front of your router, you can use the router to create routes for your app. When a request is sent to the route for your app, the request is first received by your load balancer before being forwarded to your router, which then forwards the request to your app.

1. List the details of the default router for your cluster. In the **EXTERNAL-IP** column of the output, get the worker node IP addresses that are registered for your cluster's router. In the **PORT(S)** column of the output, depending on whether you want to create a public or private load balancer, get the node port that the router service currently exposes for public or private network traffic.
    ```sh
    oc get svc router-external-default -n openshift-ingress
    ```
    {: pre}

    In the following example output, node port `30783` is exposed for public traffic (80).
    ```sh
    NAME                      TYPE           CLUSTER-IP      EXTERNAL-IP                            PORT(S)                      AGE
    router-external-default   LoadBalancer   172.21.84.172   169.xx.xxx.xxx, 169.xx.xxx.xxx         80:30783/TCP,443:30413/TCP   24h
    ```
    {: screen}

2. Using these IP addresses and the node port, create a layer 4 load balancer that is connected to your hosts' private network. For example, you might deploy a load balancer from your hosts' cloud provider, or deploy an F5 load balancer to your on-premises network. To create public routes, the load balancer must have public network connectivity and must be able to forward TCP and UDP traffic to the port for public traffic that you found in the previous step. To create private routes, the load balancer must be able to forward TCP and UDP traffic to the port for private traffic that you found in the previous step.

3. Get the **Hostname** for your cluster. This subdomain in the format `<cluster_name>-<random_hash>-0000.upi.containers.appdomain.cloud` is registered with your cluster's router.
    ```sh
    ibmcloud oc nlb-dns ls --cluster <cluster_name_or_ID>
    ```
    {: pre}

4. Add the public IP addresses of your load balancer to your cluster's subdomain. Repeat this command for all public IP addresses that you want to add.
    ```sh
    ibmcloud oc nlb-dns add --ip <public_IP> --cluster <cluster_name_or_ID> --nlb-host <hostname>
    ```
    {: pre}

5. Remove the worker node IP addresses from your cluster's subdomain. Repeat this command for all IP addresses that you retrieved earlier.
    ```sh
    ibmcloud oc nlb-dns rm classic --ip <private_IP> --cluster <cluster_name_or_ID> --nlb-host <hostname>
    ```
    {: pre}

6. Verify that the public IP addresses for your load balancer are now registered with your cluster subdomain.
    ```sh
    ibmcloud oc nlb-dns ls --cluster <cluster_name_or_ID>
    ```
    {: pre}

7. Continue with the steps in [Exposing apps with {{site.data.keyword.openshiftshort}} routes](#sat-expose-routes) to create routes for your apps.



## Exposing apps with NodePorts
{: #sat-expose-np}

If you can't use the {{site.data.keyword.openshiftshort}} router to expose an app, such as if you must expose a TCP or UDP app, you can create a [NodePort](/docs/openshift?topic=openshift-nodeport) for your app.
{: shortdesc}

1. Create a NodePort for your app. A NodePort in the range of 30000 - 32767 and an internal cluster IP address is assigned to your app.
    ```sh
    oc expose deployment <deployment_name> --type=NodePort --name=<nodeport_svc_name>
    ```
    {: pre}

2. Get the NodePort that was assigned to your app.
    ```sh
    oc describe svc <nodeport_svc_name>
    ```
    {: pre}

3. Get the **Hostname** for your cluster in the format `<cluster_name>-<random_hash>-0000.upi.containers.appdomain.cloud`.
    ```sh
    ibmcloud oc nlb-dns ls --cluster <cluster_name_or_ID>
    ```
    {: pre}

4. Access your app by using your cluster's subdomain and the NodePort in the format `<cluster_name>-<random_hash>-0000.upi.containers.appdomain.cloud:<nodeport>`. Note that if your hosts have private network connectivity only, you must be connected to the hosts' private network, such as through VPN access.

5. Optional: If you don't want to access the NodePort directly, or if you must expose your apps on a specific port such as 443, you can set up your own third-party, layer 4 load balancer that is connected to your hosts' private network and forwards traffic to the NodePort. For example, you might deploy a load balancer from your hosts' cloud provider, or deploy an F5 load balancer to your on-premises network. The load balancer must be able to forward TCP and UDP traffic for ports 30000 - 32767.



## Exposing apps with routes and Link endpoints for traffic from {{site.data.keyword.cloud_notm}}
{: #sat-expose-cloud}

If you want to access an app in your {{site.data.keyword.satelliteshort}} cluster from a resource in {{site.data.keyword.cloud_notm}} over the private network, you can use your private router to create a private route for your app. Then, you can create a Link endpoint of type `location` for the route, which is accessible only from within the {{site.data.keyword.cloud_notm}} private network.
{: shortdesc}

1. Follow the steps in [Exposing apps with {{site.data.keyword.openshiftshort}} routes](#sat-expose-routes) to create a private route for your app. This route is accessible only from within your hosts' private network.

2. Follow the steps in [Creating `location` endpoints to connect to resources in a location](/docs/satellite?topic=satellite-link-location-cloud#link-location) to create a {{site.data.keyword.satelliteshort}} Link endpoint for your app's private route.

3. Optional: To allow access to the endpoint from only the specific resource in {{site.data.keyword.cloud_notm}}, [add the resource to your endpoint's source list](/docs/satellite?topic=satellite-link-location-cloud#link-sources).






