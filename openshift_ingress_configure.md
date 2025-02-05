---

copyright:
  years: 2023, 2025
lastupdated: "2025-02-05"


keywords: ingress, configure ingress, annotations, customize ingress, ingress controller, source IP

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}

# Configuring Ingress 
{: #ingress-configure}

Learn how you can configure your Ingress setup to meet your workload needs.
{: shortdesc}


## Preserving the source IP address
{: #ingress-configure-source-ip}

To preserve source IP addresses, you can enable the PROXY protocol for VPC clusters. This option is available for clusters that run version 4.13 or later. 

The PROXY protocol provides a convenient way to transport connection information, such as a client's address, across multiple layers of NAT or TCP proxies. For more information on the PROXY protocol, see the [HAProxy specification](https://www.haproxy.org/download/1.8/doc/proxy-protocol.txt){: external}. 

By default, the Ingress controller receives connections that contain only the source address associated with the load balancer. You can enable the PROXY protocol in VPC clusters to configure the load balancer to preserve the original client address for connections that the Ingress controller receives. 

### Enabling the PROXY protocol
{: #ingress-configure-enable-proxy}

1. Edit the Ingress Controller resource.

    ```sh
    oc -n openshift-ingress-operator edit ingresscontroller/default
    ```
    {: pre}

2. In the Ingress controller resource, find the `spec.endpointPublishingStrategy.loadBalancer` section and define the following `providerParameters` values.

    ```yaml
    endpointPublishingStrategy:
      loadBalancer:
        providerParameters:
          type: IBM
          ibm:
            protocol: PROXY
        scope: External
      type: LoadBalancerService
    ```
    {: codeblock}

3. Save and apply the resource.


### Disabling PROXY protocol
{: #ingress-configure-disable-proxy}

1. Edit the Ingress Controller resource.

    ```sh
    oc -n openshift-ingress-operator edit ingresscontroller/default
    ```
    {: pre}

2. In the Ingress controller resource, find the `spec.endpointPublishingStrategy.loadBalancer` section and define the following `providerParameters` values.

    ```yaml
    endpointPublishingStrategy:
      loadBalancer:
        providerParameters:
          type: IBM
          ibm:
            protocol: TCP
        scope: External
      type: LoadBalancerService
    ```
    {: codeblock}


3. Save and apply the resource.

## Customizing Ingress routing with annotations
{: #ingress-configure-annotations}

If you want to customize routing rules for your app, you can use [route-specific HAProxy annotations](https://docs.openshift.com/container-platform/4.17/networking/routes/route-configuration.html#nw-route-specific-annotations_route-configuration){: external} in the Ingress resources that you define.

These supported annotations are in the format `haproxy.router.openshift.io/<annotation>` or `router.openshift.io/<annotation>`.{{site.data.keyword.containerlong_notm}} annotations (`ingress.bluemix.net/<annotation>`) and NGINX annotations (`nginx.ingress.kubernetes.io/<annotation>`) are not supported for the Ingress controller or the Ingress resource in {{site.data.keyword.redhat_openshift_notm}} version 4.


## Enabling access logging
{: #ingress-enable-access-logging}

HTTP access logs contain information of incoming HTTP requests. Having access logs is useful when debugging complex problems, but the OpenShift router doesn't support access logging by default. For OpenShift clusters, you can configure access logging for routers, which results in having a sidecar container in the router pod that runs a `syslog` server and writes access logs to its `stdout`.
{: shortdesc}

1. Edit the `IngressController` configuration and add the following configuration to the `.spec`.

    ```yaml
    logging:
      access:
        destination:
          type: Container
        httpCaptureHeaders:
          request:
          - maxLength: 256
            name: Host
        httpLogFormat: '{"time_date":"%t","client":"%ci","host":"%[capture.req.hdr(0)]","ssl_version":"%sslv","request_method":"%HM",
                       "request_uri":"%HU","status":%ST,"upstream_addr":"%si:%sp","request_time":%Tt,"upstream_connect_time":%Tc,
                       "upstream_header_time":%Tr,"termination_state":"%ts"}'
    ```
    {: codeblock}

    Edit command
   
    ```sh
    kubectl edit ingresscontroller -n openshift-ingress-operator default
    ingresscontroller.operator.openshift.io/default edited
    ```
    {: pre}

1. Check if the router pods are running two containers.

    ```sh
    kubectl get pod -n openshift-ingress -w
    ```
    {: pre}

    Example output

    ```sh
    NAME                              READY   STATUS    RESTARTS   AGE
    router-default-66945cc7c4-4xlnh   2/2     Running   0          36s
    router-default-66945cc7c4-5cxpn   2/2     Running   0          36s
    ```
    {: screen}

1. Check access logs.
   
    ```sh
    kubectl logs -n openshift-ingress router-default-66945cc7c4-4xlnh -c logs
    ```
    {: pre}

    Example output

    ```sh
    ...
    2025-01-28T12:29:07.038592+00:00 router-default-7fc484bbb8-qfm5d router-default-7fc484bbb8-qfm5d haproxy[41]:{"time_date":
    "28/Jan/2025:12:29:06.879","client":"10.5.207.79","host":"alb-autoscale-example-service-default.pvg-classic-z9g5zltmgb1ir
    -1e7743ca80a399c9cff4eaf617434c72-0000.us-south.stg.kube.appdomain.cloud","ssl_version":"TLSv1.3","request_method":
    "GET","request_uri":"/","status":200,"upstream_addr":"172.30.210.252:8080","request_time":159,"upstream_connect_time":1,
    "upstream_header_time":2,"termination_state":"--"}
    2025-01-28T12:29:09.572129+00:00 router-default-7fc484bbb8-qfm5d router-default-7fc484bbb8-qfm5d haproxy[41]: {"time_date":
    "28/Jan/2025:12:29:09.405","client":"10.5.207.79","host":"alb-autoscale-example-service-default.pvg-classic-z9g5zltmgb1ir
    -1e7743ca80a399c9cff4eaf617434c72-0000.us-south.stg.kube.appdomain.cloud","ssl_version":"TLSv1.3","request_method":"GET",
    "request_uri":"/","status":200,"upstream_addr":"172.30.210.252:8080","request_time":166,"upstream_connect_time":0,
    "upstream_header_time":3,"termination_state":"--"}
    ...
    ```
    {: screen}
