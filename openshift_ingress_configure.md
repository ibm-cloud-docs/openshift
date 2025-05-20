---

copyright:
  years: 2023, 2025
lastupdated: "2025-05-20"


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


## Fine-tuning connection handling
{: #ingress-configure-connection-handling}

The `clientTimeout` and `serverTimeout` parameters are crucial configurations that dictate how long connections remain active between clients, the Ingress controller, and the backend servers. These timeouts play a significant role in optimizing request handling, particularly when dealing with long-lasting client connections, delayed responses from backend servers, and safeguarding valuable resources from being unnecessarily occupied.

If you anticipate that clients will keep connections open for a longer period of time, it is advisable to increase the `clientTimeout` setting to cater to these scenarios. Conversely, if your backend servers have high latency due to high traffic volumes or processing loads, adjusting the `serverTimeout` can provide the necessary allowance for the servers to complete their request processing before the Ingress controller terminates the connection.

You can change the above parameters in your `IngressController` resource:

```yaml
apiVersion: operator.openshift.io/v1
kind: IngressController
 ...
spec:
  tuningOptions:
    clientTimeout: 5s
    serverTimeout: 5s
```
{: codeblock}

For more information about tuning options see the [OpenShift documentation](https://docs.redhat.com/en/documentation/openshift_container_platform/latest/html/operator_apis/ingresscontroller-operator-openshift-io-v1#spec-tuningoptions).
{: tip}

### Adjusting Timeouts
{: #adjusting-timeouts-oc}

If your clusters are exposed with IBM Cloud Cloud Internet Services (CIS) / Cloudflare and use Web Application Firewall (WAF) or global load balancing you should set `clientTimeout` and `serverTimeout` to values exceeding 900 seconds to prevent premature connection terminations. For more information, see the [Cloudflare documentation](https://developers.cloudflare.com/fundamentals/reference/connection-limits/#between-cloudflare-and-origin-server).
{: tip}

1. **Identify your Ingress Controller**: Begin by listing your `IngressController` resources. This can be achieved with the command:

    ```sh
    oc get ingresscontrollers -n openshift-ingress-operator
    ```
    {: pre}

2. **Update the timeout parameters**: To modify the `clientTimeout` and `serverTimeout` parameters for a specific `IngressController`, you can execute a patch command. For example the following command updates the timeout setting for the `default` Ingress Controllers to 905 seconds:

    ```sh
    oc patch ingresscontrollers default --patch '{"spec": {"tuningOptions":{"clientTimeout": "905s", "serverTimeout": "905s"}}}' --type=merge -n openshift-ingress-operator
    ```
    {: pre}

3. **VPC clusters only**: In cases where you are operating within a Virtual Private Cloud (VPC), it is neccesary to tune the idle connection timeout of the VPC load balancer along with your Ingress Controller settings. We recommend choosing a greater idle connection timeout than the timeout settings of your Ingress Controller. The command below demonstrates how to update the idle connection timeout for the `router-default` LoadBalancer service to 910 seconds:

    ```sh
    oc annotate svc -n openshift-ingress service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-idle-connection-timeout="910" router-default
    ```
    {: pre}
