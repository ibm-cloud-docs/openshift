---

copyright: 
  years: 2024, 2024
lastupdated: "2024-10-15"

keywords: private path nlb, private path network load balancer, vpc nlb, private lb
subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Setting up a Private Path Network Load Balancer for VPC
{: #setup_vpc_nlb_pp}

[Virtual Private Cloud]{: tag-vpc}
[4.16 and later]{: tag-red}

In fully private VPC environments with no public Internet access, you can use a Private Path Network Load Balancer to balance the network traffic flowing to the applications running in your VPC clusters. For more information, see the [Private Path service use cases](/docs/vpc?topic=vpc-private-path-service-intro#pps-use-cases).

Private Path Network Load Balancers for VPC are available in Beta and their functionality is subject to change.
{: beta}

## Prerequisites
{: #vpc_nlb_pp_pre}

1. [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

1. If you don't already have a running app, [deploy an app to your cluster](/docs/containers?topic=containers-deploy_app#app_cli). Ensure that you add a label in the metadata section of your deployment configuration file. This custom label identifies all pods where your app runs to include them in the load balancing.


## Configuring the `LoadBalancer` service
{: #vpc_nlb_pp_config}
{: step}

1. Copy the following`LoadBalancer` configuration and save it to a file called `lb.yaml`.
 
    ```yaml
    apiVersion: v1
    kind: Service
    metadata:
      name: <app_name>-vpc-nlb-<VPC_zone>
      annotations:
        service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-lb-name: "my-load-balancer"
        service.kubernetes.io/ibm-load-balancer-cloud-provider-enable-features: "private-path" # Required
        service.kubernetes.io/ibm-load-balancer-cloud-provider-ip-type: "private" # Required
        service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-subnets: "<subnet_ID>"
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

1. Customize the fields for your use case. For a complete list of annotations, see [Annotations and specifications](#vpc_nlb_pp_annotations).

1. Save your changes.

1. Deploy the Load Balancer service to your cluster.
    ```sh
    oc apply -f lb.yaml
    ```
    {: pre}

## Creating a Private Path service
{: #vpc_nlb_pp_setup}
{: step}

Follow the instructions to [Create a Private Path service](/docs/vpc?topic=vpc-private-path-service-about&interface=ui).

## Setting up a Virtual Private Endpoint Gateway
{: #vpc_nlb_pp_vpe}
{: step}

Now that you've configured a Load Balancer service, you must set a Virtual Private Endpoint (VPE) Gateway to access the applications in your cluster.

For more information, see [Creating an endpoint gateway in the UI](/docs/vpc?topic=vpc-ordering-endpoint-gateway&interface=ui).

## Connecting to your apps through your VPE
{: #vpc_nlb_pp_vpe}
{: step}

For information on connecting to your apps through your VPE, see [Accessing your virtual private endpoint after setting up your endpoint gateway](/docs/vpc?topic=vpc-accessing-vpe-after-setup&interface=ui).


## Annotations and specifications
{: #vpc_nlb_pp_annotations}

Review the required and optional VPC NLB annotations and specifications. 

### Required annotations and specifications
{: #vpc_nlb_pp_annotations_req}

`externalTrafficPolicy`
:   Specify `Local` or `Cluster`.
:   Set to `Local` to preserve the source IP address of client requests to your apps. This setting prevents the incoming traffic from being forwarded to a different node. This option also configures HTTP health checks.
:   If `Cluster` is set, DSR is implemented only from the worker node that the VPC NLB initially forwards the incoming request to. After the incoming request arrives, the request is forwarded to a worker node that contains the app pod, which might be in a different zone. The response from the app pod is sent to the original worker node, and that worker node uses DSR to send the response directly back to the client, bypassing the VPC NLB. This option also configures TCP health checks.


### Optional annotations and specifications
{: #vpc_nlb_pp_annotations_opt}

`service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-lb-name`
:   Include a unique name to make your VPC load balancer persistent. Persistent VPC load balancers are not deleted when the cluster they belong to is deleted. For more information, see [Persistent VPC load balancers](/docs/openshift?topic=openshift-vpclb_manage#vpc_lb_persist). This annotation can be set only on load balancer creation. It cannot be used in an update operation.

`service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-health-check-protocol`
:  This annotation sets the health check protocol on the VPC load balancer resource associated with the Kubernetes load balancer service. Available options are `http`, `https`, or `tcp`. Usually, the VPC LB health check protocol is determined by the value of the `externalTrafficPolicy` setting in the Kubernetes load balancer service specification. However, this annotation overrides that logic. This annotation does **not** alter how Kubernetes, and kube-proxy in particular, behaves in regards to the various settings of `externalTrafficPolicy`.

`service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-health-check-port`
:  The TCP port that is used for the health checks. This annotation applies only if `ibm-load-balancer-cloud-provider-vpc-health-check-protocol` is also specified. If the specified TCP port is outside of the Kubernetes node port range (30,000-32,767), the VPC security group applied to the cluster worker nodes must be modified to allow inbound traffic on the port. If this annotation is applied to a Kubernetes load balancer service associated with a VPC ALB, the outbound rules of the security group assigned to the VPC ALB must be modified to allow outbound traffic to the specified TCP port. For more information, see [Managing security groups](/docs/openshift?topic=openshift-vpc-security-group-manage).

`service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-subnets`
:   Annotation to specify which subnet to use to assigned the IP addresses for the ppNLB. These IP addresses are only used internally. The value can be a VPC subnet ID, VPC subnet name, or VPC subnet CIDR. You must specify only one subnet. All incoming traffic appears to be coming from these IP addresses. While all the addresses are in a single zone, the ppNLB still handles incoming traffic from all zones. If this specific zone goes done, incoming traffic from the other zones still works. If you don not specify this annotation, the subnet is automatically selected and the cluster worker node subnet that has the most free IP addresses available is used. To see subnets in all resource groups, run `ibmcloud oc subnets --provider vpc-gen2 --vpc-id <vpc> --zone <zone>`.


`service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-node-selector`
:   Annotation to specify a worker node label selector. You can configure specific worker nodes in your cluster to receive traffic by specifying label selector keys. You can include only one label selector in the annotation, and that the selector must be specified in the `"key=value"` format. If this annotation is not specified, all worker nodes in your cluster are configured to receive traffic from the VPC NLB. This annotation takes precedence over the `service.kubernetes.io/ibm-load-balancer-cloud-provider-zone` annotation, and any `dedicated: edge` labels on worker nodes are ignored. To limit traffic to a specific zone, you can use this annotation to specify worker nodes in that zone. Note that setting a new label on a cluster worker node does not automatically configure the worker node to receive traffic; you must recreate or update the VPC NLB for the newly labeled worker node to receive traffic.

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

`selector`
:   The label key (`<selector_key>`) and value (`<selector_value>`) that you used in the `spec.template.metadata.labels` section of your app deployment YAML. This custom label identifies all pods where your app runs to include them in the load balancing.

`port`
:   The port that the service listens on.

`targetPort`
:   Optional: The port to which the service directs traffic. The application running in the pod must be listening for incoming TCP traffic on this target port. The target port is often statically defined in the image that is running in the application pod. The target port configured in the pod is different than the node port for the service and might also be different than the external port that is configured on the VPC LB.


