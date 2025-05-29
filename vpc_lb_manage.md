---
copyright: 
  years: 2024, 2025
lastupdated: "2025-05-29"


keywords: load balancer, vpc, vpc load balancer, lb, persistent

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Managing VPC load balancers
{: #vpclb_manage}

Make changes to your existing VPC load balancers.
{: shortdesc}

Do not rename any VPC NLBs or ALBs. Renaming a VPC load balancer creates an error for the Kubernetes `LoadBalancer` service, which might disrupt your workload. 
{: important}

## Persistent VPC load balancers
{: #vpc_lb_persist}

By default, VPC load balancers are deleted when the cluster they are associated with is deleted. However, when you create a `LoadBalancer` service definition, you can make your load balancer persistent so that it remains available even after your cluster is deleted. A persistent VPC load balancer can be applied to a different cluster after its previous cluster is deleted. 
{: shortdesc}

VPC load balancer names are formatted as `kube-<cluster_ID>-<kubernetes_lb_service_UID>` by default. When a cluster is deleted, this name format specifies the associated load balancers that are then also deleted. To make sure that your load balancer is not deleted when you delete a cluster, include the `service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-lb-name` annotation in your `LoadBalancer` service definition to give your load balancer a unique name. The load balancer name must be unique within your VPC, and can include only lowercase alphanumeric characters and hyphens (`-`). The annotation can be applied to all VPC load balancer types. 

You are responsible for deleting persistent VPC load balancers when they are no longer needed. To delete a persistent VPC load balancer, delete the Kubernetes `LoadBalancer` service definition that the VPC load balancer is associated with. 

## Moving a VPC load balancer from one cluster to another
{: #vpc_lb_move}

[Persistent VPC load balancers](#vpc_lb_persist) can be detached from one VPC cluster and then attached to another. The new cluster must be within the same VPC as the original cluster.
{: shortdesc}

### Detaching a VPC load balancer from a cluster
{: #vpc_lb_move_detach}

VPC load balancers are linked to the Kubernetes `LoadBalancer` service definition that they were created with. To detach a persistent VPC load balancer from a cluster, you must break the link with the `LoadBalancer` service. Doing so makes the `LoadBalancer` service unusable, and it can be safely deleted. The VPC load balancer can then be [attached to a different cluster](#vpc_lb_move_attach). 

To break the link between the VPC load balancer and the `LoadBalancer` service, you can either [rename the VPC load balancer](/docs/vpc-infrastructure-cli-plugin?topic=vpc-infrastructure-cli-plugin-vpc-reference#load-balancer-update) or remove the `service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-lb-name` annotation from the original `LoadBalancer` service definition. Note that this is the *only* circumstance in which you should rename a VPC load balancer, as doing so creates an error for the Kubernetes resource. However, if your end goal is to use the VPC load balancer on a different cluster, this error does not disrupt your workload. Do not rename the VPC load balancer if you want to keep the load balancer on the same cluster. 

### Attaching a VPC load balancer to a cluster
{: #vpc_lb_move_attach}

After a persistent VPC load balancer is detached from a cluster, you can attach to a different cluster by creating a new Kubernetes `LoadBalancer` service definition that references the VPC load balancer.
{: shortdesc}

When you create a new `LoadBalancer` service on the new cluster, you can use the `service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-lb-name` annotation to specify the name of the VPC load balancer you want to attach.

When you create LoadBalancer service, the the VPC load balancer type (ALB, NLB) and IP type (public, private) must match the specifications in the `LoadBalancer` service. For example, an existing `LoadBalancer` service on the new cluster that specifies an NLB type cannot be used to attach a VPC ALB to the cluster. The annotations that specify the load balancer type and IP type are `service.kubernetes.io/ibm-load-balancer-cloud-provider-enable-features` and `service.kubernetes.io/ibm-load-balancer-cloud-provider-ip-type`.

The port and node ports specified in the `LoadBalancer` service do not need to match those that the VPC load balancer was created with. The VPC load balancer re-configures with the port definitions of whichever `LoadBalancer` service it is associated with in the new cluster.

## Health checks for load balancers
{: #vpc_lb_health}

VPC load balancers are automatically configured with health checks, which you configure with the `externalTrafficPolicy` annotation. You can use additional annotations to [customize health checks](#vpc_lb_health_custom) on your load balancers.
{: shortdesc} 

- If `externalTrafficPolicy` is set to `Cluster`, TCP health checks are applied. If you are configuring a UDP load balancer, [you must make additional port specifications](#vpc_lb_health_udp).
- If `externalTrafficPolicy` is set to `Local`, HTTP health checks are applied. Incoming traffic is delivered only to the application pod residing on that specific node. If there is no application pod on that specific node, the incoming traffic is dropped.

The `externalTrafficPolicy: Local` setting might cause health checks on your load balancer worker nodes to fail. Usually, this outcome is the expected behavior and does not necessarily indicate a problem, as traffic is intentionally dropped if the load balancer tries to connect to any node that does not have an application pod. For more information, see [Why are VPC load balancer health checks failing on my worker nodes?](/docs/openshift?topic=openshift-vpc-lb-healthcheck-fail).
{: note}

### Customizing health checks for VPC load balancers
{: #vpc_lb_health_custom}

For more control over your VPC load balancer health checks, you can use optional annotations to customize your health checks with advanced configurations for test intervals, timeouts, and retries. You can change or remove these customizations at any time.
{: shortdesc}

`service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-health-check-protocol`
:  **Optional**: This annotation sets the health check protocol on the VPC load balancer resource associated with the Kubernetes load balancer service. Normally, the VPC LB health check protocol is determined by the value of the `externalTrafficPolicy` setting in the Kubernetes load balancer service specification. This annotation overrides that logic. This annotation does **not** alter how Kubernetes, and kube-proxy in particular, behaves in regards to the various settings of `externalTrafficPolicy`.

`service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-health-check-port`
:  **Optional**. The TCP port that is used for the health checks. This annotation applies only if `ibm-load-balancer-cloud-provider-vpc-health-check-protocol` is also specified. 
   - If the specified TCP port is outside of the Kubernetes node port range (30,000-32,767), the VPC security group applied to the cluster worker nodes must be [modified](/docs/openshift?topic=openshift-vpc-security-group-manage) to allow inbound traffic on the port. 
   - If this annotation is applied to a Kubernetes load balancer service associated with a VPC ALB, the outbound rules of the security group assigned to the VPC ALB must be [modified](/docs/openshift?topic=openshift-vpc-security-group-manage) to allow outbound traffic to the specified TCP port. 

`service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-health-check-path`
:   **Optional**. The health check URL path for HTTP and HTTPs health checks. This annotation applies only if `ibm-load-balancer-cloud-provider-vpc-health-check-protocol` is set to `http` or `https`.
   - The URL path must be in the format of an [origin-form request target](https://www.rfc-editor.org/rfc/rfc7230#section-5.3.1){: external}.
   - If this annotation is not specified and the `ibm-load-balancer-cloud-provider-vpc-health-check-protocol` annotation is set to `http` or `https`, the  default value `/` is applied.

`service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-health-check-delay`
:   **Optional**. The number of seconds to wait between health check attempts. By default, this value is set to `5`, and has a minimum of `2` and a maximum of `60`. This value must be greater than the `ibm-load-balancer-cloud-provider-vpc-health-check-timeout` value, which is set to `2` by default. 

`service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-health-check-timeout`
:   **Optional**. The number of seconds to wait for a response to a health check. By default, this value is set to `2`, and has a minimum of `1` and a maximum of `59`. This value must be less than the `ibm-load-balancer-cloud-provider-vpc-health-check-delay` value, which is set to `5` by default. 

`service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-health-check-retries`
:   The maximum number of health check retries for the VPC load balancer. By default, this value is set to `2`, and has a minimum of `1` and a maximum of `10`.

### Enabling TCP health checks for UDP load balancers
{: #vpc_lb_health_udp}

Because there are no UDP health checks, UDP load balancers that use TCP health checks must have an additional TCP port specified with the `service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-health-check-udp` annotation. 
{: shortdesc}

You can specify the TCP node port for another load balancer or NodePort running in your cluster. For cluster 4.14 and earlier, if the node port resides outside of the `30000-32767` range, you must [modify the VPC cluster security group `kube-<cluster-ID>` to allow incoming traffic](/docs/openshift?topic=openshift-vpc-security-group-manage) to the specified port.

Note that if the specified port value is for a service that unexpectedly goes down or has its port value reconfigured, the TCP health checks stop working until the service is back up or you reconfigure the `service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-health-check-udp` annotation with a new TCP port value. To avoid this, you can specify the `kubelet` port `10250`, which is a static port value that does not experience service disruptions. However, for cluster versions 4.14 and earlier, you must [modify the VPC cluster security group `kube-<cluster-ID>`](/docs/openshift?topic=openshift-vpc-security-group-manage) to accept incoming traffic from the `kubelet` port. 

Want to avoid the complexity of specifying additional TCP ports for health checks in a UDP load balancer? Set `externalTrafficPolicy` to `Local` to use HTTP health checks, which require no additional port specifications.
{: tip}

## Changing a load balancer's subnet or zone
{: #lbaas_change_subnets}

After you have created a VPC NLB, you cannot reconfigure the listening subnet it was created with. If you want to change the listening subnet of an existing VPC NLB, you must delete, update, and reapply the corresponding Kubernetes `LoadBalancer` service.
{: shortdesc}

1. [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-access_cluster)

1. List your Kubernetes services and find the name of the `LoadBalancer` service you want to change.

    ```sh
    oc get services
    ```
    {: pre}

    Example output.

    ```sh
    NAME                     TYPE           CLUSTER-IP      EXTERNAL-IP      PORT(S)                        AGE
    my-load-balancer         LoadBalancer   172.21.77.198   52.118.150.107   8080:32767/TCP,443:30943/TCP   5d
    ```
    {: screen}

1. Find the VPC load balancer that corresponds with the Kubernetes `LoadBalancer` service.

    VPC load balancer names are in the format `kube-<cluster_ID>-<kubernetes_lb_service_UID>`. To see your cluster ID, run `ibmcloud ks cluster get --cluster <cluster_name>`. To see the Kubernetes LoadBalancer service UID, run `oc get svc <load-balancer-name> -o yaml` and look for the metadata.uid field in the output. The hyphens (-) are removed from the Kubernetes `LoadBalancer` service UID in the VPC load balancer name.
    {: tip}

    ```sh
    ibmcloud is load-balancers
    ```
    {: pre}

    Example output.

    ```sh
    ID                                          Name                                                         Family        Subnets                                       Is public   Provision status   Operating status   Resource group      
    r000-5aaaa11f6-c111-111f-b2e0-1c11aaaaf0dc0   kube-c441c43d02mb8mg00r70-3e25d0b5bf11111111fe4ca3f11111cb   Network       subnet-1                                  true        active             online             default                                                    Application      
    ```
    {: pre}


1. Get the Kubernetes `LoadBalancer` service definition and save the output as a yaml file called `my-lb.yaml`.

    ```sh
    oc describe service my-load-balancer -o yaml
    ```
    {: pre}

1. Delete the Kubernetes `LoadBalancer` service. This also deletes the corresponding VPC load balancer. 

    ```sh
    oc delete service my-load-balancer
    ```
    {: pre}

1. Update the Kubernetes `LoadBalancer` service definition file with the subnet or zone changes you want to implement. Do not change the name of the `LoadBalancer` service. For details on specifying subnets or zones for network load balancers, see [Setting up a Network Load Balancer for VPC](/docs/openshift?topic=openshift-setup_vpc_nlb).

1. Apply the new `LoadBalancer` definition file.

    ```sh
    oc apply -f my-lb.yaml
    ```

1. Verify that the Kubernetes `LoadBalancer` service is recreated successfully in your cluster. When the service is created, the **LoadBalancer Ingress** field is populated with an external IP address for the NLB.

    ```sh
    oc describe service my-load-balancer
    ```
    {: pre}

    Example output.

    ```sh
    NAME:                     my-load-balancer
    Namespace:                default
    Labels:                   <none>
    Annotations:              service.kubernetes.io/ibm-load-balancer-cloud-provider-enable-features: nlb
    Selector:                 app=echo-server
    Type:                     LoadBalancer
    IP:                       172.X.XXX.XX
    LoadBalancer Ingress:     169.XXX.XXX.XXX
    Port:                     tcp-80  80/TCP
    TargetPort:               8080/TCP
    NodePort:                 tcp-80  32022/TCP
    Endpoints:                172.XX.XX.XXX:8080,172.XX.XX.XX:8080,172.XX.XX.XX:8080 + 3 more...
    Session Affinity:         None
    External Traffic Policy:  Local
    HealthCheck NodePort:     30882
    Events:
        Type     Reason                           Age                  From                Message
    ----     ------                           ----                 ----                -------
    Normal   EnsuringLoadBalancer             9m27s (x7 over 15m)  service-controller  Ensuring load balancer
    Normal   EnsuredLoadBalancer              9m20s                service-controller  Ensured load balancer
    Normal   CloudVPCLoadBalancerNormalEvent  8m17s                ibm-cloud-provider  Event on cloud load balancer myvpcnlb for service default/my-load-balancer with UID 2d93b07d-ecf6-41d2-ad3f-9c2985122ec1: The VPC load balancer that routes requests to this Kubernetes LoadBalancer service is currently online/active.
    ```
    {: screen}


1. Verify that the VPC load balancer is recreated and that the subnet or zone is updated. Note that it takes a few minutes to provision the VPC load balancer and you might see a `create_pending` status until it is fully provisioned.

    ```sh
    ibmcloud is load-balancers
    ```
    {: pre}

    Example output.

    ```sh
    ID                                          Name                                                         Family        Subnets                                       Is public   Provision status   Operating status   Resource group     
    r006-5ecc68f6-c751-409f-b2e0-1c69babf0dc0   kube-c441c43d02mb8mg00r70-3e25d0b5bf03445796fe4ca3f73885cb   Network       subnet-2                                  true        active             online             default  
    ```
    {: pre}
