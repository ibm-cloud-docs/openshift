---

copyright:
  years: 2014, 2022
lastupdated: "2022-03-01"

keywords: openshift, route, Ingress controller

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}

# Exposing apps in {{site.data.keyword.satelliteshort}} clusters
{: #sat-expose-apps}

Securely expose apps that run in your {{site.data.keyword.satelliteshort}} cluster to traffic requests from the public network, from resources that are connected to your hosts' private network, or from resources in {{site.data.keyword.cloud_notm}}.
{: shortdesc}

You have several options for exposing apps in {{site.data.keyword.satelliteshort}} clusters:
* [MetalLB](#sat-expose-metallb): A `LoadBalancer` implementation suitable for {{site.data.keyword.satelliteshort}} clusters.
* [{{site.data.keyword.redhat_openshift_notm}} routes](#sat-expose-routes): Quickly expose apps to requests from the public or a private network with a hostname. The {{site.data.keyword.redhat_openshift_notm}} Ingress controller provides DNS registration and optional certificates for your routes.
* [Third-party load balancer and {{site.data.keyword.redhat_openshift_notm}} routes](#sat-expose-byolb): Expose apps with a hostname, and add health checking for the host IP addresses that are registered in the Ingress controller's DNS records.
* [NodePorts](#sat-expose-np): Expose non-HTTP(S) apps, such as UDP or TCP apps, with a NodePort in the 30000 - 32767 range.
* [{{site.data.keyword.redhat_openshift_notm}} routes and {{site.data.keyword.satelliteshort}} Link endpoints](#sat-expose-cloud): Expose your app with a private route, and create a Link endpoint of type `location` for the route. Only a resource that is connected to the {{site.data.keyword.cloud_notm}} private network can access your app.



## Setting up MetalLB for `LoadBalancer`s
{: #sat-expose-metallb}

"MetalLB is a load-balancer implementation for bare metal Kubernetes clusters, using standard routing protocols."
{: shortdesc}

**Prerequisites**: A dedicated subnet (AddressPool) for the external IP of the `LoadBalancer` services.

MetalLB has two components:
* A **controller** that watches `LoadBalancer` services and assigns external IPs to them from an AddressPool.
* And the **speaker** pods that hold, reply to ARP requests and handles failover of the external IPs.

**Limitations**: `externalTrafficPolicy: local` only sends traffic to the pods on the same node as the speaker that holds the external IP.

1. Verify that the MetalLB Operator is available in the {{site.data.keyword.redhat_openshift_notm}} Marketplace:
   ```sh
   oc get packagemanifests -n openshift-marketplace metallb-operator
   ```
   {: pre}

2. Create a dedicated namespace:
   ```sh
   cat << EOF | oc apply -f -
   apiVersion: v1
   kind: Namespace
   metadata:
     name: metallb-system
   EOF
   ```
   {: pre}

3. Add the operator to the cluster:
   ```sh
   cat << EOF | oc apply -f -
   apiVersion: operators.coreos.com/v1
   kind: OperatorGroup
   metadata:
     name: metallb-operator
     namespace: metallb-system
   spec:
     targetNamespaces:
     - metallb-system
   EOF
   ```
   {: pre}

4. Verify the installation:
   ```sh
   oc get operatorgroup -n metallb-system
   ```
   {: pre}

5. Subscribe to automatic updates of the operator:
   ```sh
   OC_VERSION=$(oc version -o yaml | grep openshiftVersion | grep -o '[0-9]*[.][0-9]*' | head -1)
   cat << EOF| oc apply -f -
   apiVersion: operators.coreos.com/v1alpha1
   kind: Subscription
   metadata:
     name: metallb-operator-sub
     namespace: metallb-system
   spec:
     channel: "${OC_VERSION}"
     name: metallb-operator
     source: redhat-operators
     sourceNamespace: openshift-marketplace
   EOF
   oc get installplan -n metallb-system
   ```
   {: pre}

6. Verify the subscription and operator version:
   ```sh
   oc get clusterserviceversion -n metallb-system -o custom-columns=Name:.metadata.name,Phase:.status.phase
   ```
   {: pre}

7. Enable MetalLB. Optionally limit the scope of nodes on which MetalLB speakers will be deployed, such as to a worker pool in which the dedicated subnet for the external IPs are available.
   ```sh
   cat << EOF | oc apply -f -
   apiVersion: metallb.io/v1beta1
   kind: MetalLB
   metadata:
     name: metallb
     namespace: metallb-system
   spec:
     spec:
     nodeSelector:
       ibm-cloud.kubernetes.io/worker-pool-name: edge
   EOF
   ```
   {: pre}

8. Verify the controller and speakers pods are running:
   ```sh
   oc -n metallb-system get pods -o wide
   ```
   {: pre}

9. Configure a dedicated subnet, an AddressPool for the external IP of the `LoadBalancer` services managed by MetalLB:
    ```sh
    cat << EOF | oc apply -f -
    apiVersion: metallb.io/v1alpha1
    kind: AddressPool
    metadata:
        name: doc-example-ap
        namespace: metallb-system
    spec:
        protocol: layer2
        addresses:
        - 192.0.2.0/26
        - 192.0.2.100-192.0.2.110
        - 192.0.2.200/32
    ```
    {: pre}

10. Optional: To disable auto assignment from an `AddressPool` define `autoAssign: false` in the `spec` section, in which case
    ```yaml
    metadata:
      annotations:
        metallb.universe.tf/address-pool: doc-example
    ```
    must be defined in the `LoadBalancer` service to use it.

11. To prevent IBM's Cloud Controller Manager from interacting with a MetalLB `LoadBalancer` define:
    ```yaml
    spec:
      loadBalancerClass: metallb.io
    ```
    under the `LoadBalancer` service.



## Exposing apps with {{site.data.keyword.redhat_openshift_notm}} routes
{: #sat-expose-routes}

Quickly expose the services in your cluster on the {{site.data.keyword.redhat_openshift_notm}} Ingress controller's external IP address by using a route.
{: shortdesc}

An [{{site.data.keyword.redhat_openshift_notm}} route](/docs/openshift?topic=openshift-openshift_routes) exposes a service as a hostname in the format `<service_name>-<project>.<cluster_name>-<random_hash>-0000.upi.containers.appdomain.cloud`. A Ingress controller is deployed by default to your cluster, which enables routes to be used by external clients. The Ingress controller uses the service selector to find the service and the endpoints that back the service. You can configure the service selector to direct traffic through one route to multiple services. You can also create either unsecured or secured routes by using the TLS certificate that is assigned by the Ingress controller for your hostname. Note that the Ingress controller supports only the HTTP and HTTPS protocols.

Before you begin with routes, review the following considerations.

Host network connectivity
:    If the hosts for your cluster have public network connectivity, your cluster is created with a public Ingress controller by default. You can use this Ingress controller to create public routes for your app. If the hosts for your cluster have private network connectivity only, your cluster is created with a private Ingress controller by default. You can use this Ingress controller to create private routes for your app that are accessible only from within your hosts' private network. To set up public routes in clusters that have private network connectivity only, first [set up your own third-party load balancer](#sat-expose-byolb) that has public network connectivity in front of your private Ingress controller before completing the following steps.

Health checks
:    DNS registration management is provided by default for your cluster's Ingress controller. For example, if you remove a host that was assigned to your cluster from your location and replace it with a different host, IBM updates the host IP addresses in your Ingress controller's DNS record for you. Note that while the DNS registration for routes are provided for you, no load balancer services are deployed in front of the Ingress controller in your cluster. To health check the IP addresses of the hosts that are registered in the Ingress controller's DNS records, you can [set up your own third-party load balancer](#sat-expose-byolb) in front of your Ingress controller before completing the following steps.

To create routes for your apps:

1. Create a Kubernetes `ClusterIP` service for your app deployment. The service provides an internal IP address for the app that the Ingress controller can send traffic to.
    ```sh
    oc expose deploy <app_deployment_name> --name my-app-svc
    ```
    {: pre}

2. Set up a domain for your app.
    * **IBM-provided domain**: If you don't need to use a custom domain, a route hostname is generated for you in the format `<service_name>-<project>.<cluster_name>-<random_hash>-0000.upi.containers.appdomain.cloud`. Continue to the next step.
    * **Custom domain**: Work with your DNS provider to create a custom domain. Note that if you previously set up a third-party load balancer in front of your Ingress controller, work with your DNS provider to create a custom domain for the load balancer instead.
3. Get the IP addresses for the Ingress controller service in the **EXTERNAL-IP** column.
    ```sh
    oc get svc router-external-default -n openshift-ingress
    ```
    {: pre}

4. Create a custom domain with your DNS provider. If you want to use the same subdomain for multiple services in your cluster, you can register a wildcard subdomain, such as `*.example.com`.


5. Map your custom domain to the Ingress controller's IP addresses by adding the IP addresses as A records.

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
        
    * Edge: If you use a custom domain, include `--hostname`, `--cert`, and `--key` flags, and optionally the `--ca-cert` flag. For more information about the TLS certificate requirements, see the [{{site.data.keyword.redhat_openshift_notm}} edge route documentation](https://docs.openshift.com/container-platform/4.8/networking/routes/secured-routes.html#nw-ingress-creating-an-edge-route-with-a-custom-certificate_secured-routes){: external}.
        ```sh
        oc create route edge --service <app_service_name> [--hostname <subdomain> --cert <tls.crt> --key <tls.key> --ca-cert <ca.crt>]
        ```
        {: pre}

    * Re-encrypt: If you use a custom domain, include `--hostname`, `--cert`, and `--key` flags, and optionally the `--ca-cert` flag. For more information about the TLS certificate requirements, see the [{{site.data.keyword.redhat_openshift_notm}} re-encrypt route documentation](https://docs.openshift.com/container-platform/4.8/networking/routes/secured-routes.html#nw-ingress-creating-a-reencrypt-route-with-a-custom-certificate_secured-routes){: external}.
        ```sh
        oc create route reencrypt --service <app_service_name> --dest-ca-cert <destca.crt> [--hostname <subdomain> --cert <tls.crt> --key <tls.key> --ca-cert <ca.crt>]
        ```
        {: pre}

7. Verify that the route for your app service is created.
    ```sh
    oc get routes
    ```
    {: pre}

8. Optional: Customize default routing rules with [optional configurations](https://docs.openshift.com/container-platform/4.8/networking/routes/route-configuration.html){: external}. For example, you can use [route-specific HAProxy annotations](https://docs.openshift.com/container-platform/4.8/networking/routes/route-configuration.html#nw-route-specific-annotations_route-configuration){: external}.



## Setting up a third-party load balancer in front of the {{site.data.keyword.redhat_openshift_notm}} Ingress controller
{: #sat-expose-byolb}

To health check the IP addresses of the hosts that are registered in the Ingress controller's DNS records, you can set up your own third-party load balancer in front of the IP addresses for the hosts that are assigned as worker nodes to you cluster.
{: shortdesc}

For example, if you remove a host that was assigned to your cluster from your location and replace it with a different host, IBM updates the host IP addresses in your Ingress controller's DNS record for you. But if you power off a host, such as through your cloud provider's infrastructure management, the host's IP address is not removed from your Ingress controller's DNS records and might cause a call to fail if the DNS record is resolved to that host's IP address. By setting up a load balancer in front of your Ingress controller, you can ensure that host IP addresses are regularly health checked, such as to ensure high availability for production-level workloads.

After you create a load balancer in front of your Ingress controller, you can use the Ingress controller to create routes for your app. When a request is sent to the route for your app, the request is first received by your load balancer before being forwarded to your Ingress controller, which then forwards the request to your app.

1. List the details of the default Ingress controller for your cluster. In the **EXTERNAL-IP** column of the output, get the worker node IP addresses that are registered for your cluster's Ingress controller. In the **PORT(S)** column of the output, depending on whether you want to create a public or private load balancer, get the node port that the Ingress controller service currently exposes for public or private network traffic.
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

3. Get the **Hostname** for your cluster. This subdomain in the format `<cluster_name>-<random_hash>-0000.upi.containers.appdomain.cloud` is registered with your cluster's Ingress controller.
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

7. Continue with the steps in [Exposing apps with {{site.data.keyword.redhat_openshift_notm}} routes](#sat-expose-routes) to create routes for your apps.

If you configure an external loadbalancer or VIP to register with the subdomain rather than using the default registration, that loadbalancer 
needs inbound access to the cluster hosts and the cluster hosts need outbound access to the loadbalancer. 
{: note}



## Exposing apps with NodePorts
{: #sat-expose-np}

If you can't use the {{site.data.keyword.redhat_openshift_notm}} Ingress controller to expose an app, such as if you must expose a TCP or UDP app, you can create a [NodePort](/docs/openshift?topic=openshift-nodeport) for your app.
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

If you want to access an app in your {{site.data.keyword.satelliteshort}} cluster from a resource in {{site.data.keyword.cloud_notm}} over the private network, you can use your private Ingress controller to create a private route for your app. Then, you can create a Link endpoint of type `location` for the route, which is accessible only from within the {{site.data.keyword.cloud_notm}} private network.
{: shortdesc}

1. Follow the steps in [Exposing apps with {{site.data.keyword.redhat_openshift_notm}} routes](#sat-expose-routes) to create a private route for your app. This route is accessible only from within your hosts' private network.

2. Follow the steps in [Creating `location` endpoints to connect to resources in a location](/docs/satellite?topic=satellite-link-cloud-create#link-location) to create a {{site.data.keyword.satelliteshort}} Link endpoint for your app's private route.

3. Optional: To allow access to the endpoint from only the specific resource in {{site.data.keyword.cloud_notm}}, [add the resource to your endpoint's source list](/docs/satellite?topic=satellite-link-cloud-create#link-sources).






