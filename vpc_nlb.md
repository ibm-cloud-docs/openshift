---
copyright: 
  years: 2024, 2024
lastupdated: "2024-08-16"

keywords: nlb, network load balancer, vpc nlb, dns, public lb, private lb
subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Setting up a Network Load Balancer for VPC
{: #setup_vpc_nlb}

Expose your app to the public or to the private network by setting up a public or private Kubernetes `LoadBalancer` service in each zone of your VPC cluster. Then, you can optionally [register the VPC NLB with a DNS record and TLS certificate](#vpc_nlb_dns). VPC NLBs support both the TCP and UDP protocol types. 
{: shortdesc}

## Setting up a public or private VPC NLB
{: #vpc_nlb_pub_priv}

Expose your app to network traffic by setting up a Kubernetes `LoadBalancer` service in each zone of your cluster. When you create the Kubernetes `LoadBalancer` service, a public or private Network Load Balancer for VPC (VPC NLB) that routes requests to your app is automatically created for you in your VPC outside of your cluster.
{: shortdesc}

### Before you begin
{: #vpc_nlb_before}

1. Ensure that you have the [**Writer** or **Manager** {{site.data.keyword.cloud_notm}} IAM service access role](/docs/openshift?topic=openshift-iam-platform-access-roles) for the namespace in which you deploy the Kubernetes `LoadBalancer` service for the VPC NLB.
2. [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).
3. To view VPC NLBs, install the `infrastructure-service` plug-in. The prefix for running commands is `ibmcloud is`.
    ```sh
    ibmcloud plugin install infrastructure-service
    ```
    {: pre}
4. **For private VPC NLBs**: Connect to your VPC private network, such as through a [VPC VPN connection](/docs/openshift?topic=openshift-vpc-vpnaas).
5. **For private VPC NLBs**: Enable your app to receive private network requests.
    1. [Create a VPC subnet](https://cloud.ibm.com/vpc/network/subnets){: external} that is dedicated to your VPC NLB. This subnet must exist in the same VPC and location as your cluster, but can't be attached to your cluster or any worker nodes. If you enter a specific IP range, don't use the following reserved ranges: `172.16.0.0/16`, `172.18.0.0/16`, `172.19.0.0/16`, and `172.20.0.0/16`. After you provision the subnet, note its **ID**.
    2. If the client that connects to your app through the VPC NLB exists outside of the VPC and zone of your dedicated VPC subnet, you must [create a custom ingress routing table](https://cloud.ibm.com/vpc-ext/network/routingTables){: external}. For more information, see the table in the [known limitations](/docs/vpc?topic=vpc-nlb-limitations) and [About routing tables and routes](/docs/vpc?topic=vpc-about-custom-routes).
        Select one of the following **Traffic sources** for your custom ingress routing table: For traffic from an on-premise netowrk, choose  **Direct link**. For traffic from another VPC or from classic infrastructure, choose **Transit gateway**. For traffic from another zone within the same VPC, choose **VPC zone**. For more information, see [Setting up VPC VPN connectivity](/docs/openshift?topic=openshift-vpc-vpnaas).
        {: note}


### Configure the `LoadBalancer` service
{: #vpc_nlb_config}

1. [Deploy your app to the cluster](/docs/containers?topic=containers-deploy_app#app_cli). Ensure that you add a label in the metadata section of your deployment configuration file. This custom label identifies all pods where your app runs to include them in the load balancing.

2. Create a configuration YAML file for your Kubernetes `LoadBalancer` service. In the YAML file, specify the `service.kubernetes.io/ibm-load-balancer-cloud-provider-ip-type` annotation as either `"public"` or `"private"`. The `annotations` section in the example file includes only some of the available annotations. For a complete list of required and optional VPC NLB annotations, see [Annotations and specifications](#vpc_nlb_annotations).

    To make your VPC NLB easily identifiable, consider naming the service in the format `<app_name>-vpc-nlb-<VPC_zone>`.
    {: tip}
    
    ```yaml
    apiVersion: v1
    kind: Service
    metadata:
      name: <app_name>-vpc-nlb-<VPC_zone>
      annotations:
        service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-lb-name: "my-load-balancer"
        service.kubernetes.io/ibm-load-balancer-cloud-provider-enable-features: "nlb"
        service.kubernetes.io/ibm-load-balancer-cloud-provider-ip-type: "public"
        service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-node-selector: "<key>=<value>"
        service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-subnets: "<subnet1_ID,subnet2_ID>"
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
    oc apply -f <filename>.yaml -n <namespace>
    ```
    {: pre}

4. Verify that the Kubernetes `LoadBalancer` service is created successfully in your cluster. When the service is created, the **LoadBalancer Ingress** field is populated with an external IP address that is assigned by the VPC NLB.

    **The VPC NLB takes a few minutes to provision in your VPC.** The external IP address of your Kubernetes `LoadBalancer` service might be `pending` until the VPC NLB is fully provisioned.
    {: note}

    ```sh
    oc describe svc myloadbalancer -n <namespace>
    ```
    {: pre}

    Example CLI output for a public `LoadBalancer` service:
    ```sh
    NAME:                     myapp-vpc-nlb-us-east
    Namespace:                default
    Labels:                   <none>
    Annotations:              service.kubernetes.io/ibm-load-balancer-cloud-provider-enable-features: nlb
    Selector:                 app=echo-server
    Type:                     LoadBalancer
    IP:                       172.21.204.12
    LoadBalancer Ingress:     169.XXX.XXX.XXX
    Port:                     tcp-80  80/TCP
    TargetPort:               8080/TCP
    NodePort:                 tcp-80  32022/TCP
    Endpoints:                172.17.17.133:8080,172.17.22.68:8080,172.17.34.18:8080 + 3 more...
    Session Affinity:         None
    External Traffic Policy:  Local
    HealthCheck NodePort:     30882
    Events:
        Type     Reason                           Age                  From                Message
    ----     ------                           ----                 ----                -------
    Warning  SyncLoadBalancerFailed           13m (x5 over 15m)    service-controller  Error syncing load balancer: failed to ensure load balancer: kube-bqcssbbd0bsui62odcdg-2d93b07decf641d2ad3f9c2985122ec1 for service default/myvpcnlb is busy: offline/create_pending
    Normal   EnsuringLoadBalancer             9m27s (x7 over 15m)  service-controller  Ensuring load balancer
    Normal   EnsuredLoadBalancer              9m20s                service-controller  Ensured load balancer
    Normal   CloudVPCLoadBalancerNormalEvent  8m17s                ibm-cloud-provider  Event on cloud load balancer myvpcnlb for service default/myvpcnlb with UID 2d93b07d-ecf6-41d2-ad3f-9c2985122ec1: The VPC load balancer that routes requests to this Kubernetes LoadBalancer service is currently online/active.
    ```
    {: screen}

5. Verify that the VPC NLB is created successfully in your VPC. In the output, verify that the VPC NLB has an **Operating Status** of `online` and a **Provision Status** of `active`.

    ```sh
    ibmcloud is load-balancers
    ```
    {: pre}

    In the following example CLI output, the VPC NLB that is named `kube-bh077ne10vqpekt0domg-046e0f754d624dca8b287a033d55f96e` is created for the Kubernetes `LoadBalancer` service:
    ```sh
    ID                                     Name                                                         Created          Host Name                                  Is Public   Listeners                               Operating Status   Pools                                   Private IPs              Provision Status   Public IPs                    Subnets                                Resource Group
    06496f64-a689-4693-ba23-320959b7b677   kube-bh077ne10vqpekt0domg-046e0f754d624dca8b287a033d55f96e   8 minutes ago    1234abcd-us-south.lb.appdomain.cloud       yes         95482dcf-6b9b-4c6a-be54-04d3c46cf017    online             717f2122-5431-403c-b21d-630a12fc3a5a    10.241.0.7               active             169.63.99.184                 c6540331-1c1c-40f4-9c35-aa42a98fe0d9   00809211b934565df546a95f86160f62
    ```
    {: screen}

6. Access the IP address of the Kubernetes `LoadBalancer` service that you found in step 4 and your app port in the format `<external_IP>:<app_port>`.

7. Optional: Repeat these steps to deploy a public VPC NLB in each zone where you want to expose your app. Then, you can register the external IP addresses of the VPC NLB in each zone with one [DNS subdomain](#vpc_nlb_dns).

Do not delete the subnets that you attached to your cluster during cluster creation or when you add worker nodes in a zone. If you delete a VPC subnet that your cluster used, any VPC NLBs that use IP addresses from the subnet might experience issues, and you might be unable to create new load balancers.
{: important}

### Setting up a public NLB using a port range
{: #nlb-setup-portrange}

Port ranges can be used in  public NLBs when there is a need to host a service from a single host name that has multiple backend applications, each listening on a separate port number. To use port ranges in your Kubernetes cluster, some manual configuration must be performed. First, the `ibm-load-balancer-cloud-provider-vpc-port-range` option must be set.  It can include one or multiple ranges, each delimited by a comma. The `spec.ports.port` value must also be set to the minimum value in the port range.

In the following example, a port range of `30000-30010` is used.


Nodeport services must be manually created for each deployment in which the NLB service forwards the request. The port number of each of these Nodeport services must be within the port range that is configured in the NLB service.

In the following example diagram, a Nodeport service with port 30000 is created for Deployment 1 while a Nodeport service with port 30001 is created for Deployment 2.

The user makes a request to port 30001 of the NLB containing the port range. This request is directed to the VPC NLB service that directs the request to the Nodeport service in the cluster that is also listening on port 30001, which in this case is for Deployment 2. The Nodeport service then directs the request to the target port of the selected pods of Deployment 2.

![VPC NLB that uses port range.](/images/nlb-port-range.svg){: caption="Figure 3. VPC NLB with port range" caption-side="bottom"}

Create an NLB that uses a port range by using the following example. The selector and backend pods must be associated with the port range load balancer service so that health checks return success and data is delivered to the ports in the port range. To use port range, you must create additional NodePort services that have port values in the range that is defined by the load balancer service.

1. Save the following example `LoadBalancer` configuration as a file called `loadbalancer.yaml`.

    ```yaml
    apiVersion: v1
    kind: Service
    metadata:
      annotations:
        service.kubernetes.io/ibm-load-balancer-cloud-provider-enable-features: nlb
        service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-port-range: 30000-30010
      name: nlb-port-range
    spec:
      externalTrafficPolicy: Cluster
      ports:
      - port: 30000 # Must match min from the port range 
        protocol: TCP
        nodePort: 30011 # Can be port in range or not
        targetPort: 8080
      selector:
        app: echo-server  # Must be valid for health checks to work
      type: LoadBalancer
    ```
    {: codeblock}
    
1. Create the service.
    ```sh
    oc apply -f loadbalancer.yaml
    ```
    {: pre}

1. Create a `NodePort` service with port values that are in the port range specified in the `LoadBalancer` you created earlier.

    ```yaml
    apiVersion: v1
    kind: Service
    metadata:
      name: echo-server-node-port
    spec:
      ports:
      - port: 80
        protocol: TCP # The protocol of the port range
        nodePort: 30003 # Node port in the port range
        targetPort: 8080
      selector:
        app: echo-server
      type: NodePort
    ```
    {: codeblock}

1. Create the NodePort service.

    ```sh
    oc apply -f nodeport.yaml
    ```
    {: pre}

1. To access a port that is in the range provided by NLB.
    ```sh
    curl https://<public ip assigned to NLB>:30003
    ```
    {: pre}

    - `30003` = Is a node port in the range that responds to request
    - Other ports in the range do not respond unless additional node port services are created.


## Annotations and specifications
{: #vpc_nlb_annotations}

Review the required and optional VPC NLB annotations and specifications. 

### Required annotations and specifications
{: #vpc_nlb_annotations_req}

`service.kubernetes.io/ibm-load-balancer-cloud-provider-enable-features: "nlb"`
:   Annotation to create a VPC NLB. If you do not include this annotation and specify `nlb`, a VPC ALB is created by default. 

`service.kubernetes.io/ibm-load-balancer-cloud-provider-ip-type: "private"`
:   (Required for private NLBs) Annotation to specify a service that accepts private requests. If this annotation is not included, a public VPC NLB is created.
  
`service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-subnets`
:   (Required for private NLBs, optional for public NLBs) Annotation to specify the dedicated subnet that the VPC NLB deploys to. The value can be specified as a VPC subnet ID, VPC subnet name, or VPC subnet CIDR. You must specify only one subnet. The subnet must exist in the same VPC as your cluster and in a zone where your cluster has worker nodes, but no worker nodes can be attached to this subnet. The worker nodes that exist in the same zone as this subnet are configured to receive traffic from the VPC NLB. To see subnets in all resource groups, run `ibmcloud oc subnets --provider vpc-gen2 --vpc-id <vpc> --zone <zone>`.

`externalTrafficPolicy`
:   Specify `Local` or `Cluster`.
:   Set to `Local` to preserve the source IP address of client requests to your apps. This setting prevents the incoming traffic from being forwarded to a different node. This option also configures HTTP health checks.
:   If `Cluster` is set, DSR is implemented only from the worker node that the VPC NLB initially forwards the incoming request to. After the incoming request arrives, the request is forwarded to a worker node that contains the app pod, which might be in a different zone. The response from the app pod is sent to the original worker node, and that worker node uses DSR to send the response directly back to the client, bypassing the VPC NLB. This option also configures TCP health checks. For UDP load balancers, the `service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-health-check-udp` is required if you choose the `Cluster` option. For more information, see [Configuring TCP health checks for UDP load balancers](#vpc_lb_health_udp).


### Optional annotations and specifications
{: #vpc_nlb_annotations_opt}

`service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-lb-name`
:   Include a unique name to make your VPC load balancer persistent. Persistent VPC load balancers are not deleted when the cluster they belong to is deleted. For more information, see [Persistent VPC load balancers](#vpc_lb_persist). This annotation can be set only on load balancer creation. It cannot be used in an update operation.

`service.kubernetes.io/ibm-load-balancer-cloud-provider-zone`
:   Annotation to specify a VPC zone that your cluster is attached to. The VPC NLB is deployed to the same subnet in that zone that your worker nodes are connected to.  If you later change this annotation to a different zone, the VPC NLB is not moved to the new zone. If you don't specify this annotation or the `service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-subnets annotation`, the VPC NLB is deployed to the most optimal zone (such as a zone that has worker nodes in the `Ready` state). If the `dedicated: edge` label is set on worker nodes and you specify this annotation, then only edge nodes in the specified zone are configured to receive traffic. Edge nodes in other zones and non-edge nodes in the specified zone don't receive traffic from the load balancer. To see zones, run `ibmcloud ks zone ls --provider vpc-gen2`. To see zones, run `ibmcloud ks zone ls --provider vpc-gen2`.

`service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-node-selector`
:   Annotation to specify a worker node label selector. You can configure specific worker nodes in your cluster to receive traffic by specifying label selector keys. You can include only one label selector in the annotation, and that the selector must be specified in the `"key=value"` format. If this annotation is not specified, all worker nodes in your cluster are configured to receive traffic from the VPC NLB. This annotation takes precedence over the `service.kubernetes.io/ibm-load-balancer-cloud-provider-zone` annotation, and any `dedicated: edge` labels on worker nodes are ignored. To limit traffic to a specific zone, you can use this annotation to specify worker nodes in that zone. Note that setting a new label on a cluster worker node does not automatically configure the worker node to recieve traffic; you must recreate or update the VPC NLB for the newly-labeled worker node to recieve traffic. 

`service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-health-check-udp`
:    The TCP node port to use for TCP health checks in a UDP load balancer. Required for UDP load balancers that have `externalTrafficPolicy` set to `Cluster`. See [Configuring TCP health checks for UDP load balancers](#vpc_lb_health_udp) for more considerations before setting a port value.

`service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-health-check-protocol`
:  This annotation sets the health check protocol on the VPC load balancer resource associated with the Kubernetes load balancer service. Available options are `http`, `https`, or `tcp`. Usually, the VPC LB health check protocol is determined by the value of the `externalTrafficPolicy` setting in the Kubernetes load balancer service specification. However, this annotation overrides that logic. This annotation does **not** alter how Kubernetes, and kube-proxy in particular, behaves in regards to the various settings of `externalTrafficPolicy`.

`service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-health-check-port`
:  The TCP port that is used for the health checks. This annotation applies only if `ibm-load-balancer-cloud-provider-vpc-health-check-protocol` is also specified. If the specified TCP port is outside of the Kubernetes node port range (30,000-32,767), the VPC security group applied to the cluster worker nodes must be [modified](/docs/openshift?topic=openshift-vpc-security-group-manage) to allow inbound traffic on the port. If this annotation is applied to a Kubernetes load balancer service associated with a VPC ALB, the outbound rules of the security group assigned to the VPC ALB must be [modified](/docs/openshift?topic=openshift-vpc-security-group-manage) to allow outbound traffic to the specified TCP port. 

`service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-health-check-path`
:   The health check URL path for HTTP and HTTPs health checks. This annotation applies only if `ibm-load-balancer-cloud-provider-vpc-health-check-protocol` is set to `http` or `https`. The URL path must be in the format of an [origin-form request target](https://www.rfc-editor.org/rfc/rfc7230#section-5.3.1){: external}. If this annotation is not specified and the `ibm-load-balancer-cloud-provider-vpc-health-check-protocol` annotation is set to `http` or `https`, the  default value `/` is applied.

`service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-health-check-delay`
:   **Optional**. The number of seconds to wait between health check attempts. By default, this value is set to `5`, and has a minimum of `2` and a maximum of `60`. This value must be greater than the `ibm-load-balancer-cloud-provider-vpc-health-check-timeout` value, which is set to `2` by default. 

`service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-health-check-timeout`
:   **Optional**. The number of seconds to wait for a response to a health check. By default, this value is set to `2`, and has a minimum of `1` and a maximum of `59`. This value must be less than the `ibm-load-balancer-cloud-provider-vpc-health-check-delay`, which is set to `5` by default. 

`service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-health-check-retries`
:   The maximum number of health check retries for the VPC load balancer. By default, this value is set to `2`, and has a minimum of `1` and a maximum of `10`.








`service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-member-quota`
:   Optional. The number of worker nodes per zone that the load balancer routes to. The default value is 8. For a cluster with worker nodes in three zones, this results in the the load balancer routing to 24 total worker nodes. The total number of worker nodes across all zones that the load balancer routes to cannot exceed 50. If the cluster has fewer than 50 worker nodes across all zones, specify 0 to route to all worker nodes in a zone. 

`service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-allow-outbound-traffic`
:   Available for clusters that run [Secure by Default](/docs/containers?topic=openshift-vpc-security-group-reference). Annotation to create security groups for each IP address of an ALB associated with an external port that you specify. These rules are created in the cluster security group. Specify valid external ports in a comma-separated list, such as `80,443`. In this example, if each public ALB associated with each external port value has two IP addresses, one outbound rule is created per IP address for a total of 4 new rules. You can add or remove this annotation at any time.

`selector`
:   The label key (`<selector_key>`) and value (`<selector_value>`) that you used in the `spec.template.metadata.labels` section of your app deployment YAML. This custom label identifies all pods where your app runs to include them in the load balancing.

`port`
  :   The port that the service listens on.

`targetPort`
:   Optional: The port to which the service directs traffic. The application running in the pod must be listening for incoming TCP traffic on this target port. The target port is often statically defined in the image that is running in the application pod. The target port configured in the pod is different than the node port for the service and might also be different than the external port that is configured on the VPC LB.


