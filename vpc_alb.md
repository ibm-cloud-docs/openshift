---
copyright: 
  years: 2024, 2024
lastupdated: "2024-09-17"

keywords: alb, application load balancer, vpc alb, dns, public lb, private lb

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Setting up an Application Load Balancer for VPC
{: #setup_vpc_alb}

Expose your app to the public or to the private network by setting up a Kubernetes `LoadBalancer` service in your cluster. When you expose your app, an Application Load Balancer for VPC (VPC ALB) that routes requests to your app is automatically created for you in your VPC outside of your cluster. Then, you can optionally [register the VPC ALB with a DNS record and TLS certificate](#vpc_lb_dns). VPC ALBs support the TCP protocol only. 
{: shortdesc}

Do not confuse the Application Load Balancer for VPC with {{site.data.keyword.openshiftlong_notm}} Ingress applications load balancers. Application Load Balancers for VPC (VPC ALBs) run outside your cluster in your VPC and are configured by Kubernetes `LoadBalancer` services that you create. [Ingress applications load balancers (ALBs)](/docs/containers?topic=containers-comm-ingress-annotations) are Ingress controllers that run on worker nodes in your cluster.
{: note}

## Setting up a public or private VPC ALB
{: #setup_vpc_alb_pub_priv}

Before you begin

- Ensure that you have the [**Writer** or **Manager** {{site.data.keyword.cloud_notm}} IAM service access role](/docs/openshift?topic=openshift-iam-platform-access-roles) for the namespace in which you deploy the Kubernetes `LoadBalancer` service for the VPC ALB.
- [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).
- To view VPC ALBs, install the `infrastructure-service` plug-in. The prefix for running commands is `ibmcloud is`.
    ```sh
    ibmcloud plugin install infrastructure-service
    ```
    {: pre}


To enable your app to receive public or private request:

1. [Deploy your app to the cluster](/docs/openshift?topic=openshift-app). Ensure that you add a label in the metadata section of your deployment configuration file. This custom label identifies all pods where your app runs to include them in the load balancing.

2. Create a configuration YAML file for your Kubernetes `LoadBalancer` service. In the YAML file, specify the `service.kubernetes.io/ibm-load-balancer-cloud-provider-ip-type` annotation as either `"public"` or `"private"`. The `annotations` section in the example file includes only some available annotations. For a complete list of required and optional VPC ALB annotations, see [Annotations and specifications](#vpc_alb_annotations).

    To make your VPC ALB easily identifiable, consider naming the service in the format `<app_name>-vpc-alb-<VPC_zone>`.
    {: tip}
    

    ```yaml
    apiVersion: v1
    kind: Service
    metadata:
      name: myloadbalancer
      annotations:
        service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-lb-name: "`<app_name>-vpc-alb-<VPC_zone>`"
        service.kubernetes.io/ibm-load-balancer-cloud-provider-enable-features: "proxy-protocol"
        service.kubernetes.io/ibm-load-balancer-cloud-provider-ip-type: "<public_or_private>"
        service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-node-selector: "<key>=<value>"
   spec:
     type: LoadBalancer
     selector:     
        <selector_key>: <selector_value>
     ports:
       - name: http
         protocol: TCP
         port: 8080
         targetPort: 8080 # Optional. By default, the `targetPort` is set to match the `port` value unless specified otherwise. 
       - name: https
         protocol: TCP
         port: 443
         targetPort: 443 # Optional. By default, the `targetPort` is set to match the `port` value unless specified otherwise. 
      externalTrafficPolicy: Local # Specify Local or Cluster. 
    ```
    {: codeblock}

3. Create the Kubernetes `LoadBalancer` service in your cluster.
    ```sh
    oc apply -f myloadbalancer.yaml -n <namespace>
    ```
    {: pre}

4. Verify that the Kubernetes `LoadBalancer` service is created successfully in your cluster. When the service is created, the **LoadBalancer Ingress** field is populated with a hostname that is assigned by the VPC ALB.

    **The VPC ALB takes a few minutes to provision in your VPC.** You can't access your app by using the hostname of your Kubernetes `LoadBalancer` service until the VPC ALB is fully provisioned.
    {: note}

    ```sh
    oc describe svc myloadbalancer -n <namespace>
    ```
    {: pre}

    Example CLI output for a public `LoadBalancer` service:
    ```sh
    NAME:                     myvpcalb
    Namespace:                default
    Labels:                   <none>
    Annotations:              
    Selector:                 app=echo-server
    Type:                     LoadBalancer
    IP:                       172.21.XX.XX
    LoadBalancer Ingress:     1234abcd-us-south.lb.appdomain.cloud
    Port:                     tcp-80  80/TCP
    TargetPort:               8080/TCP
    NodePort:                 tcp-80  30610/TCP
    Endpoints:                172.17.17.133:8080,172.17.22.68:8080,172.17.34.18:8080 + 3 more...
    Session Affinity:         None
    External Traffic Policy:  Local
    HealthCheck NodePort:     31438
    Events:
        Type    Reason                           Age   From                Message
    ----    ------                           ----  ----                -------
    Normal  EnsuringLoadBalancer             16m   service-controller  Ensuring load balancer
    Normal  EnsuredLoadBalancer              15m   service-controller  Ensured load balancer
    Normal  CloudVPCLoadBalancerNormalEvent  13m   ibm-cloud-provider  Event on cloud load balancer myvpcalb for service default/myvpcalb with UID 08cbacf0-2c93-4186-84b6-c4ab88a2faf9: The VPC load balancer that routes requests to this Kubernetes LoadBalancer service is currently online/active.
    ```
    {: screen}

5. Verify that the VPC ALB is created successfully in your VPC. In the output, verify that the VPC ALB has an **Operating Status** of `online` and a **Provision Status** of `active`.

    ```sh
    ibmcloud is load-balancers
    ```
    {: pre}

    In the following example CLI output, the VPC ALB that is named `kube-bsaucubd07dhl66e4tgg-1f4f408ce6d2485499bcbdec0fa2d306` is created for the Kubernetes `LoadBalancer` service:
    ```sh
    ID                                          Name                                                         Family        Subnets               Is public   Provision status   Operating status   Resource group
    r006-d044af9b-92bf-4047-8f77-a7b86efcb923   kube-bsaucubd07dhl66e4tgg-1f4f408ce6d2485499bcbdec0fa2d306   Application   mysubnet-us-south-3   true        active             online             default
    ```
    {: screen}

6. If you created a public `LoadBalancer` service, curl the hostname of the Kubernetes `LoadBalancer` service that is assigned by the VPC ALB that you found in step 4.
    Example:
    ```sh
    curl 06496f64-us-south.lb.appdomain.cloud:8080
    ```
    {: pre}

    Example output

    ```sh
    Hello world from hello-world-deployment-5fd7787c79-sl9hn! Your app is up and running in a cluster!
    ```
    {: screen}

    If you created a private `LoadBalancer` service, you must be [connected to your private VPC network](/docs/vpc?topic=vpc-vpn-onprem-example) to curl the hostname.
    {: tip}

Do not delete the subnets that you attached to your cluster during cluster creation or when you add worker nodes in a zone. If you delete a VPC subnet that your cluster used, any load balancers that use IP addresses from the subnet might experience issues, and you might be unable to create new load balancers.
{: important}

VPC ALBs and NLBs that are not tied to Kubernetes or Openshift clusters can be updated directly by using 'ibmcloud is' commands or the **VPC Infrastructure** section in the console. For example, change a front-end listener's port or health check timeout value. But for VPC load balancers that are tied to Kubernetes or Openshift clusters, any updates to them must be performed via annotations in the Ingress configuration. The IBM Cloud Provider periodically re-syncs with any associated VPC ALBs and NLBs to ensure the running load balancer conforms to the Ingress's expected configuration. So if you make any changes to such a load balancer directly via VPC instead of using Ingress annotations, those changes will be reverted back.
{: important}

## Registering a DNS record and TLS certificate
{: #vpc_lb_dns}

The Application Load Balancer for VPC (VPC ALB) provides a default HTTP hostname in the format `1234abcd-<region>.lb.appdomain.cloud` through which you can access your app. However, if you want a TLS certificate for your app domain to support HTTPS, you can create an IBM-provided subdomain or bring your own custom domain for both public and private VPC ALBs.
{: shortdesc}

After you create a DNS subdomain for a VPC ALB hostname, you can't use `nlb-dns health-monitor` commands to create a custom health check. Instead, the default VPC load balancer health check that is provided for the default VPC ALB hostname is used. For more information, see the [VPC documentation](/docs/vpc?topic=vpc-alb-health-checks).
{: note}

Before you begin

- [Set up a VPC ALB](#setup_vpc_alb). Ensure that you define an HTTPS port in your Kubernetes `LoadBalancer` service that configures the VPC ALB.
- To use the TLS certificate to access your app via HTTPS, your app must be able to terminate TLS connections.

To register a VPC ALB hostname with a DNS subdomain:

1. Retrieve the hostname for your VPC ALB by running the `get svc` command. In the output, look for the hostname in the **EXTERNAL-IP** column. For example, `1234abcd-us-south.lb.appdomain.cloud`. 
    ```sh
    oc get svc -o wide
    ```
    {: pre}

    Example output

    ```sh
    NAME            TYPE           CLUSTER-IP       EXTERNAL-IP                            PORT(S)     AGE       SELECTOR
    ...
    webserver-lb    LoadBalancer   172.21.xxx.xxx   1234abcd-us-south.lb.appdomain.cloud   8080:30532/TCP     1d       run=webserver
    ```
    {: screen}

2. Create a custom or IBM-provided DNS subdomain for the load balancer hostname.
    - **Custom domain**: Provide your own custom domain and give it an alias by specifying the load balancer external IP, in the format `1234abcd-us-south.lb.appdomain.cloud` as a Canonical Name record (CNAME).
        1. Register a custom domain by working with your Domain Name Service (DNS) provider or [{{site.data.keyword.cloud_notm}} DNS](/docs/dns-svcs?topic=dns-svcs-getting-started).
        2. Define an alias for your custom domain by specifying the load balancer external IP as a Canonical Name record (CNAME). In the following example, the load balancer with the external IP of `1234abcd-us-south.lb.appdomain.cloud` is reachable at `www.your-custom-domain.com`.
        
        Host/Service
        :   The prefix where you want to reach your app such as, `www`.
        
        Resource Type
        :   Select `CNAME`.
        
        TTL
        :   Select a time to live.
        
        Value/Target
        :   The LoadBalancer external IP that you retrieved earlier. For example `1234abcd-us-south.lb.appdomain.cloud.`. Note that when using {{site.data.keyword.cloud_notm}} DNS, make sure to enter a trailing period.

    - **IBM-provided subdomain**: Use `nlb-dns` commands to generate a subdomain with a TLS certificate for the VPC ALB hostname. {{site.data.keyword.cloud_notm}} takes care of generating and maintaining the wildcard TLS certificate for the subdomain for you.
        1. Create a DNS subdomain and TLS certificate.
            ```sh
            ibmcloud oc nlb-dns create vpc-gen2 --cluster <cluster_name_or_id> --lb-host <vpc_lb_hostname> --type (public|private)
            ```
            {: pre}
            
        2. Verify that the subdomain is created. For more information, see [Understanding the subdomain format](/docs/openshift?topic=openshift-loadbalancer_hostname#loadbalancer_hostname_format).
            ```sh
            ibmcloud oc nlb-dns ls --cluster <cluster_name_or_id>
            ```
            {: pre}

            Example output
            ```sh
            Subdomain                                                                               Load Balancer Hostname                        Health Monitor   SSL Cert Status           SSL Cert Secret Name
            mycluster-a1b2cdef345678g9hi012j3kl4567890-0001.us-south.containers.appdomain.cloud     ["1234abcd-us-south.lb.appdomain.cloud"]      None             created                   <certificate>
            ```
            {: screen}

3. If you created a subdomain for a public VPC ALB, open a web browser and enter the URL to access your app through the subdomain such as the example `www.your-custom-domain.com`. If you created a subdomain for a private VPC ALB, you must be [connected to your private VPC network](/docs/vpc?topic=vpc-vpn-onprem-example) to test access to your subdomain.

To use the TLS certificate to access your app via HTTPS, ensure that you defined an HTTPS port in your [Kubernetes `LoadBalancer` service](#setup_vpc_alb). You can verify that requests are correctly routing through the HTTPS port by running `curl -v --insecure https://<domain>`. A connection error indicates that no HTTPS port is open on the service. Also, ensure that TLS connections can be terminated by your app. You can verify that your app terminates TLS properly by running `curl -v https://<domain>`. A certificate error indicates that your app is not properly terminating TLS connections.
{: tip}

### Registering a private DNS record for a private VPC ALB
{: #vpc_alb_private_dns}

 In version 4.15 or later you can use the following optional annotations to associate an own DNS `instance` which serves a custom DNS `zone` with a private VPC ALB. For this both optional annotations must be set.
If they are unspecified then DNS `A` records for this load balancer's `hostname` property will be added to the public DNS zone `lb.appdomain.cloud`.

`service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-private-dns-instance-crn: "private-dns-crn"`
    :   The DNS `instance` to associate with this load balancer. The specified instance may be in a different region or account, subject to IAM policies.
    Possible values: 9 ≤ length ≤ 512

`service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-private-dns-zone-id: "dns-zone-id"`
    :   The DNS `zone` to associate with this load balancer. The specified zone may be in a different region or account, subject to IAM policies.
    Possible values: 1 ≤ length ≤ 128, Value must match regular expression ^[a-z0-9\-]*[a-z0-9]$

You need to do the following as pre requirement before you can use this feature:
* Create the DNS zone which can be bound to a load balancer
* Enable service-to-service authorization between VPC LBs and DNS Services
* Add the cluster's VPC to the permitted networks of the zone

For detailed informations see the [Integrating an application load balancer with IBM Cloud DNS Services](/docs/vpc?topic=vpc-lb-dns) and [Add a VPC as a permitted network to the DNS zone](/docs/dns-svcs?topic=dns-svcs-getting-started#step-4-add-vpc-as-permitted-network-to-dns-zone) documents.

Example:
```yaml
apiVersion: v1
kind: Service
metadata:
  name: myloadbalancer
  annotations:
    service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-lb-name: "my-load-balancer"
    service.kubernetes.io/ibm-load-balancer-cloud-provider-ip-type: "private"
    service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-private-dns-instance-crn: "crn:v1:bluemix:public:dns-svcs:global:a/bb1b52262f7441a586f49068482f1e60:f761b566-030a-4696-8649-cc9d09889e88::"
    service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-private-dns-zone-id: "d66662cc-aa23-4fe1-9987-858487a61f45"
spec:
  type: LoadBalancer
status:
  loadBalancer:
    ingress:
    - ip: 169.60.115.164
...
```
{: codeblock}


## Annotations and specifications
{: #vpc_alb_annotations}

Review the required and optional VPC ALB annotations and specifications. 

### Required annotations and specifications
{: #vpc_alb_annotations_req}

`service.kubernetes.io/ibm-load-balancer-cloud-provider-enable-features: "alb"`
:   Annotation to create a VPC ALB. If you do not include `service.kubernetes.io/ibm-load-balancer-cloud-provider-enable-features`, a VPC ALB is provisioned by default. 

`service.kubernetes.io/ibm-load-balancer-cloud-provider-ip-type: "private"`
:   (Required for private VPC ALBs) Annotation to specify a service that accepts public or private requests. If this annotation is not included, a public VPC ALB is created.

`externalTrafficPolicy`
:   Specify `Cluster` to forward a request to a worker node that contains the app pod. This worker node might be in a different zone. By default, this annotation is set to `Cluster`.
:   Specify `Local` to prevent the incoming traffic from forwarding to a different node. This option also configures HTTP health checks. 
:   Note that to use the original client source IP for VPC ALBs, you must enable the PROXY protocol with the `service.kubernetes.io/ibm-load-balancer-cloud-provider-enable-features: "proxy-protocol"` annotation. 

### Optional annotations and specifications
{: #vpc_alb_annotations_opt}

`service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-lb-name`
:   Include a unique name to make your VPC load balancer persistent. Persistent VPC load balancers are not deleted when the cluster they belong to is deleted. For more information, see [Persistent VPC load balancers](/docs/openshift?topic=openshift-vpclb_manage#vpc_lb_persist). This annotation can be set only on load balancer creation. It cannot be used in an update operation.

`service.kubernetes.io/ibm-load-balancer-cloud-provider-enable-features: "proxy-protocol"`
:   Enable the PROXY protocol. The load balancer passes client connection information, including the client IP address, the proxy server IP address, and both port numbers, in request headers to your back-end app. Note that your back-end app must be configured to accept the PROXY protocol. For example, you can configure an NGINX app to accept the PROXY protocol by following [these steps](https://docs.nginx.com/nginx/admin-guide/load-balancer/using-proxy-protocol/){: external}.

`service.kubernetes.io/ibm-load-balancer-cloud-provider-zone`
:   Annotation to specify a VPC zone that your cluster is attached to. When you specify a zone in this annotation, two processes occur: (1) The VPC ALB is deployed to the same subnet in that zone that your worker nodes are connected to, and (2) only worker nodes in your cluster in this zone are configured to receive traffic from the VPC ALB. To place the load balancer in a specific zone, you must specify this annotation when you create the load balancer. If you later change this annotation to a different zone, the listening and backend worker nodes are automatically updated to match the new zone. If the `dedicated: edge` label is set on worker nodes and you specify this annotation, then only edge nodes in the specified zone are configured to receive traffic. Edge nodes in other zones and non-edge nodes in the specified zone don't receive traffic from the load balancer. To see zones, run `ibmcloud ks zone ls --provider vpc-gen2`.

`service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-subnets`
:   Annotation to specify one or more subnets that the VPC ALB service deploys to. If specified, this annotation takes precedence over the `service.kubernetes.io/ibm-load-balancer-cloud-provider-zone` annotation. Without this annotation, the subnets that the VPC ALB deploys to automatically update to match the zones of a cluster if the cluster is updated from single zone to multi-zone, or vice versa. Note that you can specify a different subnet in the same VPC than the subnets that your cluster is attached to. In this case, even though the VPC ALB deploys to a different subnet in the same VPC, the VPC ALB can still route traffic to your worker nodes on the cluster subnets. To see subnets in all resource groups, run `ibmcloud oc subnets --provider vpc-gen2 --vpc-id <vpc> --zone <zone>`. This annotation can be added or modified for existing VPC ALBs. 

`service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-node-selector`
:   Annotation to specify a worker node label selector.  You can configure specific worker nodes in your cluster to receive traffic by specifying label selector keys. You can include only one label selector in the annotation, and that the selector must be specified in the `"key=value"` format. If this annotation is not specified, all worker nodes in your cluster are configured to receive traffic from the VPC ALB. This annotation takes precedence over the `service.kubernetes.io/ibm-load-balancer-cloud-provider-zone` annotation, and any `dedicated: edge` labels on worker nodes are ignored. To limit traffic to a specific zone, you can use this annotation to specify worker nodes in that zone. Note that setting a new label on a cluster worker node does not automatically configure the worker node to receive traffic; you must recreate or update the VPC ALB for the newly labeled worker node to receive traffic. 

`service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-health-check-protocol`
:   The health check protocol on the VPC load balancer resource associated with the Kubernetes load balancer service. Available options are `http`, `https`, or `tcp`. Usually, the VPC LB health check protocol is determined by the value of the `externalTrafficPolicy` setting in the Kubernetes load balancer service specification, however this annotation overrides that logic. This annotation does **not** alter how Kubernetes, and kube-proxy in particular, behaves in regards to the various settings of `externalTrafficPolicy`.

`service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-health-check-port`
:   The TCP port that is used for the health checks. This annotation applies only if `ibm-load-balancer-cloud-provider-vpc-health-check-protocol` is also specified. 
:   If your cluster does not run [Secure by Default](/docs/openshift?topic=openshift-vpc-security-group-reference), you might need to make the following modifications to the VPC security groups applied. If your cluster does run Secure by Default, these changes are applied automatically. 
:   - If the specified TCP port is outside of the Kubernetes node port range (30,000-32,767), the VPC security group applied to the cluster worker nodes must be [modified](/docs/openshift?topic=openshift-vpc-security-group-manage) to allow inbound traffic on the port.
:   - If this annotation is applied to a Kubernetes load balancer service associated with a VPC ALB, the outbound rules of the security group assigned to the VPC ALB must be [modified](/docs/openshift?topic=openshift-vpc-security-group-manage) to allow outbound traffic to the specified TCP port. 

`service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-health-check-path`
:   The health check URL path for HTTP and HTTPs health checks. This annotation applies only if `ibm-load-balancer-cloud-provider-vpc-health-check-protocol` is set to `http` or `https`. The URL path must be in the format of an [origin-form request target](https://www.rfc-editor.org/rfc/rfc7230#section-5.3.1){: external}. If this annotation is not specified and the `ibm-load-balancer-cloud-provider-vpc-health-check-protocol` annotation is set to `http` or `https`, the  default value `/` is applied.

`service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-health-check-delay`
:   The number of seconds to wait between health check attempts. By default, this value is set to `5`, and has a minimum of `2` and a maximum of `60`. This value must be greater than the `ibm-load-balancer-cloud-provider-vpc-health-check-timeout` value, which is set to `2` by default. 

`service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-health-check-timeout`
:   The number of seconds to wait for a response to a health check. By default, this value is set to `2`, and has a minimum of `1` and a maximum of `59`. This value must be less than the `ibm-load-balancer-cloud-provider-vpc-health-check-delay`, which is set to `5` by default.

`service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-health-check-retries`
:   The maximum number of health check retries for the VPC load balancer. By default, this value is set to `2`, and has a minimum of `1` and a maximum of `10`.

`service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-idle-connection-timeout`
:   The idle connection timeout of the listener in seconds. The default idle timeout is dependent on your account settings. Usually, this value is `50`. However, some allowlisted accounts have larger timeout settings. If you don't set the annotation, your loadbalancers use the timeout setting in your account. You can explicitly specify the timeout by setting this annotation. The minimum is `50`. The maximum is `7200`.


`service.kubernetes.io/ibm-load-balancer-cloud-provider-dns-name: "example-ingress-domain.<region>.containers.appdomain.cloud"`
:   Version 4.16 or later.
:   Register the load balancer's IP address with the specified [Ingress domain](/docs/openshift?topic=openshift-ingress-domains). If the specified domain does not exist, a domain is created that uses the internal, IBM managed provider (`akamai`). To create a new domain, the name must be unique across all existing domains (not just those on your cluster). Deleting the load balancer service removes the IP address from the domain. However, removing the annotation does not remove the IP address from the domain. 






`service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-private-dns-instance-crn: "private-dns-crn"`
:   Version 4.15 or later.
:   The DNS `instance` to associate with this load balancer.  For more information, see [Registering a private DNS record](#vpc_alb_private_dns).


`service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-private-dns-zone-id: "dns-zone-id"`
:   Version 4.15 or later.
:   The DNS `zone` to associate with this load balancer. For more information, see [Registering a private DNS record](#vpc_alb_private_dns).

`service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-member-quota`
:  The number of worker nodes per zone that the load balancer routes to. The default value is 8. For a cluster with worker nodes in three zones, this results in the the load balancer routing to 24 total worker nodes. The total number of worker nodes across all zones that the load balancer routes to cannot exceed 50. If the cluster has fewer than 50 worker nodes across all zones, specify 0 to route to all worker nodes in a zone. 



`service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-allow-outbound-traffic`
:   Available for clusters that run [Secure by Default](/docs/openshift?topic=openshift-vpc-security-group-reference). Annotation to create security groups for each IP address of an ALB associated with an external port that you specify. These rules are created in the cluster security group and automatically update if the VPC ALB IP address changes. Specify valid external ports in a comma-separated list, such as `80,443`. In this example, if each public ALB associated with each external port value has two IP addresses, one outbound rule is created per IP address for a total of 4 new rules. You can add or remove this annotation at any time.

`selector`
:   The label key (`<selector_key>`) and value (`<selector_value>`) that you used in the `spec.template.metadata.labels` section of your app deployment YAML. This custom label identifies all pods where your app runs to include them in the load balancing.

`port`
:   The port that the service listens on.

`targetPort`
:   The port to which the service directs traffic. The application running in the pod must be listening for incoming TCP traffic on this target port. The target port is often statically defined in the image that is running in the application pod. The target port configured in the pod is different than the node port for the service and might also be different than the external port that is configured on the VPC LB.
