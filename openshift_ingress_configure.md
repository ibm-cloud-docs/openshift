---

copyright:
  years: 2023, 2023
lastupdated: "2023-05-17"

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
    {: pre}

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
    {: pre}

3. Save and apply the resource.

## Customizing Ingress routing with annotations
{: #ingress-configure-annotations}

If you want to customize routing rules for your app, you can use [route-specific HAProxy annotations](https://docs.openshift.com/container-platform/4.11/networking/routes/route-configuration.html#nw-route-specific-annotations_route-configuration){: external} in the Ingress resources that you define.

These supported annotations are in the format `haproxy.router.openshift.io/<annotation>` or `router.openshift.io/<annotation>`.{{site.data.keyword.containerlong_notm}} annotations (`ingress.bluemix.net/<annotation>`) and NGINX annotations (`nginx.ingress.kubernetes.io/<annotation>`) are not supported for the Ingress controller or the Ingress resource in {{site.data.keyword.redhat_openshift_notm}} version 4.



