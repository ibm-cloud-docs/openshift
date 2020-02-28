---

copyright:
  years: 2014, 2020
lastupdated: "2020-02-27"

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
{: help}
{: support}

Use the router to publicly expose the services in your {{site.data.keyword.openshiftlong}} cluster on the router's external IP address by using a route.
{: shortdesc}

## Overview
{: #routes-overview}

A router is deployed by default to your cluster and functions as the ingress point for external network traffic. The router listens on the public host network interface, unlike your app pods that listen only on private IPs. The router uses the service selector to find the service and the endpoints that back the service, and creates [routes](https://docs.openshift.com/container-platform/4.3/networking/routes/route-configuration.html){: external} that expose services as hostnames to be used by external clients. You can configure the service selector to direct traffic through one route to multiple services. You can also create either unsecured or secured routes by using the TLS certificate that is assigned by the router for your hostname. After you set up routes for your services, the router proxies external requests for route hostnames that you associate with services. Requests are sent to the IPs of the app pods that are identified by the service. Note that the router supports only the HTTP and HTTPS protocols.

If you have a multizone cluster, one router is deployed to your cluster, and a router service is created in each zone. Note that the router service in the first zone where you have workers nodes is always named `router-default` in 4.3 clusters or `router` in 3.11 clusters, and router services in zones that you subsequently add to your cluster have names such as `router-dal12`.
* To see the router services in each zone of your cluster, run `oc get svc -n openshift-ingress`.
* To see the router subdomain for your cluster and the IP addresses for the router service in each zone, run `ibmcloud oc nlb-dns ls -c <cluster_name_or_ID>` and looking for the subdomain formatted like `<cluster_name>-<random_hash>-0000.<region>.containers.appdomain.cloud`.

Not sure whether to use OpenShift routes or Ingress? Check out [Choosing among load balancing solutions](/docs/openshift?topic=openshift-cs_network_planning#routes-vs-ingress).
{: tip}

### Traffic flow in a single-zone cluster
{: #route_single}

The following diagram shows how a router directs communication from the internet to an app in a single-zone cluster.
{: shortdesc}

<img src="images/roks-router.png" alt="Expose an app in a single-zone OpenShift cluster by using a router" width="550" style="width:550px; border-style: none"/>

1. A request to your app uses the route hostname that you set up for your app. A DNS system service resolves the subdomain to the floating public IP address of router service.

2. The router service receives the request and forwards it to the private IP address of the app pod over the private network. The source IP address of the request package is changed to the public IP address of the worker node where the router pod runs. If multiple app instances are deployed in the cluster, the router sends the requests between the app pods.

3. When the app returns a response packet, it uses the IP address of the worker node where the router that forwarded the client request exists. The router then sends the response packet through the load balancer service to the client.

### Traffic flow in a multizone cluster
{: #route_multi}

The following diagram shows how a router directs communication from the internet to an app in a multizone cluster.
{: shortdesc}

<img src="images/roks-router-multi.png" alt="Expose an app in a multizone OpenShift cluster by using a router" width="700" style="width:700px; border-style: none"/>

1. A request to your app uses the route hostname that you set up for your app.

2. A DNS system service resolves the route subdomain to the floating public IP address of a router service. Requests are handled by the router services in various zones in a round-robin cycle.

3. The router receives the request and forwards it to the private IP address of the app pod over the private network. The source IP address of the request package is changed to the public IP address of the worker node where the router pod runs. Each router sends requests to the app instances in its own zone and to app instances in other zones. Additionally, if multiple app instances are deployed in one zone, the router sends the requests between the app pods in the zone.

4. When the app returns a response packet, it uses the IP address of the worker node where the router that forwarded the client request exists. The router then sends the response packet through the load balancer service to the client.

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
  * IBM-provided domain: If you do not need to use a custom domain, a route subdomain is generated for you in the format `<service_name>-<project>.<cluster_name>-<random_hash>-0000.<region>.containers.appdomain.cloud`.
  * Custom domain: To specify a custom domain, work with your DNS provider or [{{site.data.keyword.cis_full}}](https://cloud.ibm.com/catalog/services/internet-services).
    1. Get the public IP address for the default public router service in each zone in the **EXTERNAL-IP** column. Note that the router service in the first zone where you have workers nodes is always named `router-default` in 4.3 clusters or `router` in 3.11 clusters, and router services in zones that you subsequently add to your cluster have names such as `router-dal12`.
      * Version 3.11 clusters:
        ```
        oc get svc router
        ```
        {: pre}
      * Version 4.3 and later clusters:
        ```
        oc get svc -n openshift-ingress
        ```
        {: pre}
    2. Create a custom domain with your DNS provider.
        If you want to use the same subdomain for multiple services in your cluster, you can register a wildcard subdomain, such as `*.example.com`.
        {: tip}
    3. Map your custom domain to the router's public IP address by adding the IP address as an A record.

3. [Set up a route](https://docs.openshift.com/container-platform/4.3/cli_reference/openshift_cli/developer-cli-commands.html#expose){: external}.
  * If you do not have a custom domain, do not specify a **Hostname** value. A route subdomain is generated for you in the format `<service_name>-<project>.<cluster_name>-<random_hash>-0000.<region>.containers.appdomain.cloud`.
  * If you registered a wildcard subdomain, specify a unique subdomain in each route resource that you create. For example, you might specify `svc1.example.com` in this route resource, and `svc2.example.com` in another route resource.

4. Verify that the route for your app is created.
  ```
  oc get routes
  ```
  {: pre}

5. Optional: Customize default routing rules with [optional configurations](https://docs.openshift.com/container-platform/4.3/networking/routes/route-configuration.html){: external}. For example, you can use [HAProxy annotations for the OpenShift router](https://docs.openshift.com/container-platform/4.3/networking/routes/route-configuration.html#nw-route-specific-annotations_route-configuration){: external}.

<br />




## Setting up routes to privately expose your apps
{: #private-routes-setup}

To use routes to privately expose your apps, create a new router and change the service that exposes the router to a private load balancer. The router service is assigned an IP address through which private requests are forwarded to your app.
{: shortdesc}

<img src="images/icon-version-311.png" alt="Version 3.11 icon" width="30" style="width:30px; border-style: none"/> Private routes are supported for clusters that run OpenShift version 3.11 only. Private routes are currently not supported for clusters that run OpenShift version 4.3 or later. Instead, you can [create a private network load balancer (NLB)](/docs/openshift?topic=openshift-loadbalancer).
{: note}

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

3. Change the `router-private` service that exposes the router to a private load balancer.
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

4. Verify that the `router-private` service has a **TYPE** of `LoadBalancer` and note the **EXTERNAL-IP** address.
    ```
    oc get svc | grep router-private
    ```
    {: pre}

    Example output:
    ```
    NAME                     TYPE           CLUSTER-IP       EXTERNAL-IP     PORT(S)                                     AGE
    router-private           LoadBalancer   172.21.XXX.XX    10.XX.XX.XX     80:31554/TCP,443:30329/TCP,1936:32477/TCP   2m
    ```
    {: screen}

5. To have an external endpoint for your private router, you must register your private router service's external IP address with a custom domain.
    1. Create a custom domain. To register your custom domain, work with your Domain Name Service (DNS) provider or [{{site.data.keyword.cloud_notm}} DNS](/docs/dns?topic=dns-getting-started).
        If you want to use the same subdomain for multiple services in your cluster, you can register a wildcard subdomain, such as `*.example.com`.
        {: tip}
    2. Map your custom domain to the private router service's external IP address by adding the IP address as an A record.

6. Update the project where your app and private router are deployed to use the private router instead of the default public router.
  ```
  oc label namespace <project> "router=router-private"
  ```
  {: pre}

7. Restart the pods for the private router.
  ```
  oc scale dc/router-private --replicas=0 -n <project> && oc scale dc/router-private --replicas=2 -n <project>
  ```
  {: pre}

8. Create a Kubernetes `ClusterIP` service for your app deployment. The service provides an internal IP address for the app that the router can send traffic to.
  ```
  oc expose deploy <app_deployment_name> --name my-app-svc
  ```
  {: pre}

9. [Set up a route](https://docs.openshift.com/container-platform/4.3/cli_reference/openshift_cli/developer-cli-commands.html#expose){: external}. If you do not specify a **Hostname** value and you registered the router service with a private DNS entry in step 4, a route hostname is generated for you in the format `<app_service_name>-<project>.<custom_domain>`.

10. Verify that the route for your app is created.
  ```
  oc get routes
  ```
  {: pre}

11. Optional: Customize the private router's routing rules with [optional configurations](https://docs.openshift.com/container-platform/4.3/networking/routes/route-configuration.html){: external}. For example, you can use [HAProxy annotations for the OpenShift router](https://docs.openshift.com/container-platform/4.3/networking/routes/route-configuration.html#nw-route-specific-annotations_route-configuration){: external}.

## Moving router services across VLANs
{: #migrate-router-vlan}

When you [change your worker node VLAN connections](/docs/openshift?topic=openshift-cs_network_cluster#change-vlans), the worker nodes are connected to the new VLAN and assigned new public or private IP addresses. However, router services cannot automatically migrate to the new VLAN because they are assigned a stable, portable public or private IP address from a subnet that belongs to the old VLAN. When your worker nodes and routers are connected to different VLANs, the routers cannot forward incoming network traffic to app pods to your worker nodes. To move your router services to a different VLAN, you must create the router service on the new VLAN and delete the router service on the old VLAN.
{: shortdesc}

1. Create a router service on the new VLAN.
  * **<img src="images/icon-version-311.png" alt="Version 3.11 icon" width="30" style="width:30px; border-style: none"/> Version 3.11 clusters**:
    1. Describe the configuration for the default public router service. In the output, copy the `prometheus.openshift.io/password: xxxxxxxxxx` annotation, and any custom annotations that you manually added to the router. Do not copy other annotations.<p class="note>Note that the router service in the first zone where you have workers nodes is always named `router` in 3.11 clusters, and router services in the zones that you subsequently add to your cluster have names such as `router-dal12`.</p>
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

  * **<img src="images/icon-version-43.png" alt="Version 4.3 icon" width="30" style="width:30px; border-style: none"/> Version 4.3 and later clusters**:
    1. Create a YAML configuration file for a new router service. Specify the zone that the router service deploys to. Save the file as `router-new.yaml`.
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
          router: router-default
        name: router-new
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

    2. Create the new router service.
      ```
      oc apply -f router-new.yaml -n openshift-ingress
      ```
      {: pre}

    3. Get the **EXTERNAL-IP** address of the new router service. This IP address is from a subnet on the new VLAN.
      ```
      oc get svc router-new -n openshift-ingress
      ```
      {: pre}

      Example output:
      ```
      NAME                         TYPE           CLUSTER-IP       EXTERNAL-IP     PORT(S)                                     AGE
      router-new                   LoadBalancer   172.21.XX.XX     169.XX.XXX.XX   80:31049/TCP,443:30219/TCP                  2m
      ```
      {: screen}

2. Note the **Hostname** and **IP** address of the router. In the output, look for the hostname formatted like `<cluster_name>-<random_hash>-0001.<region>.containers.appdomain.cloud`. The IP address that is listed is the IP for the service that exposes the router on the old VLAN.
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

3. Add the IP address of the new router service that you found in step 1 to the router's hostname. Your router service on the new VLAN is now registered with the domain for the default router in your cluster, and can forward incoming requests to apps.
  ```
  ibmcloud oc nlb-dns add -c <cluster_name_or_ID> --ip <new_IP> --nlb-host <subdomain>
  ```
  {: pre}

4. Remove the IP address of the old router service that you found in step 2 from the router's hostname.
  ```
  ibmcloud oc nlb-dns rm classic -c <cluster_name_or_ID> --ip <old_IP> --nlb-host <hostname>
  ```
  {: pre}

5. Verify that the hostname for your router is now registered with the new IP address. After your router hostname is updated with the IP address of the new service, no further changes to your router or routes are required.
  ```
  ibmcloud oc nlb-dns ls -c <cluster_name_or_ID>
  ```
  {: pre}

6. Delete the router service on the old VLAN.
  * Version 3.11:
    ```
    oc delete svc <old_router_svc>
    ```
    {: pre}
  * Version 4.3 and later:
    ```
    oc delete svc <old_router_svc> -n openshift-ingress
    ```
    {: pre}

7. Optional: If you no longer need the subnets on the old VLANs, you can [remove them](/docs/openshift?topic=openshift-subnets#remove-subnets).
