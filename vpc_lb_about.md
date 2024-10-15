---

copyright: 
  years: 2014, 2024
lastupdated: "2024-10-15"


keywords: kubernetes, openshift, app protocol, application protocol

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# About VPC load balancers
{: #vpclb-about}

[Virtual Private Cloud]{: tag-vpc}

Learn how you can use VPC load balancers to expose your app on the public or private network.
{: shortdesc}

To expose an app in a VPC cluster, you can create a layer 7 VPC Application Load Balancer (VPC ALB) or a layer 4 VPC Network Load Balancer (VPC NLB). 

If you create a **public** Kubernetes `LoadBalancer` service, you expose your app to public network traffic. You can access your app from the internet through the external, public IP address that is assigned by the VPC NLB to the Kubernetes `LoadBalancer` service. No public gateway is required on your VPC subnet to allow public requests to your VPC NLB. However, if your app must access a public URL, you must attach public gateways to the VPC subnets that your worker nodes are connected to.

If you create a **private** Kubernetes `LoadBalancer` service, you expose your app to private network traffic. Your app is accessible only to systems that are connected to your private subnets within the same region and VPC. If you are connected to your private VPC network, you can access your app through the external, private IP address that is assigned by the VPC NLB to the Kubernetes `LoadBalancer` service.

## Load balancer types
{: #vpclb-types}



The following table describes the basic characteristics of each load balancing option.



| Characteristic | Application Load BalancerA (ALB) | Network Load Balancer (NLB) | Private Path NLB |
|--------------|---------------------|-----------------------------|
| Supported {{site.data.keyword.redhat_openshift_notm}} version | All versions | All versions | 4.16 and later |
| Transport layer | Layer 7 | Layer 4 | Layer 4 |
| Types of load balancers | Public and private | Public and private | Private |
| Supported protocols | TCP | TCP, UDP | TCP |
| Application access | Hostname | Hostname and static IP address | Only via VPE gateway |
| Source IP preservation | Configurable | Yes | No |
| Improved performance with direct server return | No | Yes | Yes |
| Multizone routing | Yes | Backend pool only | Yes |
| Port ranges | No | Public only | Yes |
| Security groups | Yes | Yes | No |
{: caption="Load balancing options for VPC clusters"}




### Application load balancer for VPC
{: #vpc-alb}

Set up a layer-7, multizone [Application Load Balancer for VPC](/docs/vpc?topic=vpc-load-balancers) (VPC ALB) to serve as the external entry point for incoming requests to an app in your cluster. Keep the following points in mind when planning your VPC ALB setup. 
{: shortdesc}

Do not confuse the Application Load Balancer for VPC with {{site.data.keyword.openshiftlong_notm}} Ingress applications load balancers. Application Load Balancers for VPC (VPC ALBs) run outside your cluster in your VPC and are configured by Kubernetes `LoadBalancer` services that you create. [Ingress applications load balancers (ALBs)](/docs/containers?topic=containers-comm-ingress-annotations) are Ingress controllers that run on worker nodes in your cluster.
{: note}

* VPC ALB names have a format `kube-<cluster_ID>-<kubernetes_lb_service_UID>`. To see your cluster ID, run `ibmcloud oc cluster get --cluster <cluster_name>`. To see the Kubernetes `LoadBalancer` service UID, run `oc get svc myloadbalancer -o yaml` and look for the **metadata.uid** field in the output. The hyphens (-) are removed from the Kubernetes `LoadBalancer` service UID in the VPC ALB name.

* By default, when you create a Kubernetes `LoadBalancer` service for an app in your cluster, an Application Load Balancer for VPC is created in your VPC outside of your cluster. The VPC ALB routes requests to your app through the private NodePorts that are automatically opened on your worker nodes.

* If you create a **public** Kubernetes `LoadBalancer` service, you can access your app from the internet through the hostname that is assigned by the VPC ALB to the Kubernetes `LoadBalancer` service in the format `1234abcd-<region>.lb.appdomain.cloud`. Even though your worker nodes are connected to only a private VPC subnet, the VPC ALB can receive and route public requests to the service that exposes your app. Note that no public gateway is required on your VPC subnet to allow public requests to your VPC ALB. However, if your app must access a public URL, you must attach public gateways to the VPC subnets that your worker nodes are connected to.

* If you create a **private** Kubernetes `LoadBalancer` service, your app is accessible only to systems that are connected to your private subnets within the same region and VPC. If you are connected to your private VPC network, you can access your app through the hostname that is assigned by the VPC ALB to the Kubernetes `LoadBalancer` service in the format `1234abcd-<region>.lb.appdomain.cloud`.

* You can use an existing VPC ALB on a different cluster by renaming the VPC ALB. 

The following diagram illustrates how a user accesses an app from the internet through the VPC ALB.

![Load balancing for a cluster through the VPC ALB.](images/vpc-alb-mz.svg){: caption="Load balancing for a cluster through the VPC ALB" caption-side="bottom"}

1. A request to your app uses the hostname that is assigned to the Kubernetes `LoadBalancer` service by the VPC ALB, such as `1234abcd-<region>.lb.appdomain.cloud`.
2. The request is automatically forwarded by the VPC ALB to one of the node ports on the worker node, and then to the private IP address of the app pod.
3. If app instances are deployed to multiple worker nodes in the cluster, the load balancer routes the requests between the app pods on various worker nodes. Additionally, if you have a multizone cluster, the VPC ALB routes requests to worker nodes across all subnets and zones in your cluster.

### Network load balancer for VPC
{: #vpc-nlb}

In VPC clusters, set up a layer-4 [Network Load Balancer for VPC](/docs/vpc?topic=vpc-network-load-balancers) (VPC NLB) in each zone of your cluster to serve as the external entry point for incoming requests to an app.
{: shortdesc}

VPC NLBs provide several advantages, such as providing higher throughput and better performance by utilizing direct server return (DSR). With DSR, the worker node can send app response packets directly to the client IP address and skip the VPC NLB, decreasing the amount of traffic that the VPC NLB must handle. Additionally, you can configure the VPC NLB to include source IP address preservation on all client requests by including the [`externalTrafficPolicy: Local` specification](/docs/containers?topic=containers-setup_vpc_nlb#vpc_nlb_annotations). 

* Standard VPC NLB names have a format `kube-<cluster_ID>-<kubernetes_lb_service_UID>`. To see your cluster ID, run `ibmcloud oc cluster get --cluster <cluster_name>`. To see the Kubernetes `LoadBalancer` service UID, run `oc get svc myloadbalancer -o yaml` and look for the **metadata.uid** field in the output. The hyphens (-) are removed from the Kubernetes `LoadBalancer` service UID in the VPC NLB name.

* When you create a Kubernetes `LoadBalancer` service for an app in your cluster and include the `service.kubernetes.io/ibm-load-balancer-cloud-provider-enable-features: "nlb"` annotation, a VPC NLB is created in your VPC outside of your cluster. The VPC NLB routes requests for your app through the private NodePorts that are automatically opened on your worker nodes.

* If you create a **public** Kubernetes `LoadBalancer` service, you can access your app from the internet through the external, public IP address that is assigned by the VPC NLB to the Kubernetes `LoadBalancer` service. Even though your worker nodes are connected to only a private VPC subnet, the VPC NLB can receive and route public requests to the service that exposes your app. Note that no public gateway is required on your VPC subnet to allow public requests to your VPC NLB. However, if your app must access a public URL, you must attach public gateways to the VPC subnets that your worker nodes are connected to.

* If you create a **private** Kubernetes `LoadBalancer` service, your app is accessible only to systems that are connected to your private subnets within the same region and VPC. If you are connected to your private VPC network, you can access your app through the external, private IP address that is assigned by the VPC NLB to the Kubernetes `LoadBalancer` service.


The following diagram illustrates how a user accesses an app from the internet through the VPC NLB.

![Load balancing for a cluster through the VPC NLB.](/images/vpc-nlb-sz.svg){: caption="VPC load balancing for a cluster through the VPC NLB" caption-side="bottom"}

1. A request to your app uses the external IP address that is assigned to the Kubernetes `LoadBalancer` service by the VPC NLB.
2. The request is automatically forwarded by the VPC NLB to one of the node ports on the worker node, and then to the private IP address of the app pod.
3. If app instances are deployed to multiple worker nodes in the cluster, the VPC NLB routes the requests between the app pods on various worker nodes across all zones of the cluster.



## Limitations
{: #vpclb_limit}

Review the following default settings and limitations.
{: shortdesc}

* Review [known limitations for VPC ALBs](/docs/vpc?topic=vpc-lb-limitations) and [known limitations for VPC NLBs](/docs/vpc?topic=vpc-nlb-limitations).
* Private VPC ALBs don't accept all traffic, only RFC 1918 traffic.
* Private VPC NLBs must be created on a dedicated VPC subnet that must exist in the same VPC and location as your cluster, but the subnet can't be attached to your cluster or any worker nodes.
* {{site.data.keyword.redhat_openshift_notm}}: Although the Kubernetes [SCTP protocol](https://kubernetes.io/docs/concepts/services-networking/service/#sctp){: external} is generally available in the Kubernetes community release, creating load balancers that use this protocol is not supported in {{site.data.keyword.containerlong_notm}} clusters.
* One VPC load balancer is created for each Kubernetes `LoadBalancer` service that you create, and it routes requests to that Kubernetes `LoadBalancer` service only. Across all your VPC clusters in your VPC, a maximum of 50 VPC load balancers can be created. For more information, see the [VPC quotas documentation](/docs/vpc?topic=vpc-quotas).
* The VPC load balancer can route requests to a limited number of worker nodes. The maximum number of nodes you can route requests to depends on how you set the `externalTrafficPolicy` annotation. 
    * If you set `externalTrafficPolicy: Cluster` in your load balancer configuration:
        * The VPC load balancer routes to the first 8 worker nodes that are discovered in each zone. For a cluster with worker nodes in three zones, this results in the load balancer routing to 24 worker nodes total. For a single-zone cluster, the load balancer routes to 8 worker nodes total. You can change the number of worker nodes per zone that the load balancer routes to with the `service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-member-quota`, but the total number across all zones cannot exceed 50. If the cluster has fewer than 50 worker nodes across all zones, specify 0 to route to all worker nodes in a zone. The `kube-proxy` configures IP tables to route the incoming traffic from the worker node to the application pod on whichever node the application pod resides on. 
    * If you set `externalTrafficPolicy: Local` in your load balancer configuration, the VPC load balancer is created only if there are 50 or fewer worker nodes on the cluster. This limit is set by VPC quota limitations of 50 pool members per VPC load balancer pool. To avoid this limitation, use the `service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-node-selector` annotation to limit which worker nodes are in the load balancer pool. For instance, you can use this annotation to force incoming traffic to a specific worker pool. If you use this annotation to force traffic to a specific worker pool, you must also ensure that the application pod also runs in the same worker pool. 
* When you define the configuration YAML file for a Kubernetes `LoadBalancer` service, the following annotations and settings are not supported:
    * `service.kubernetes.io/ibm-load-balancer-cloud-provider-vlan: "<vlan_id>"`
    * `service.kubernetes.io/ibm-load-balancer-cloud-provider-enable-features: "ipvs"`
    * `service.kubernetes.io/ibm-load-balancer-cloud-provider-ipvs-scheduler: "<algorithm>"`
    * `spec.loadBalancerIP`
    * `spec.loadBalancerSourceRanges`
    * VPC NLBs only: `service.kubernetes.io/ibm-load-balancer-cloud-provider-enable-features: "proxy-protocol"`
    * VPC ALBs only: The `externalTrafficPolicy: Local` setting is supported, but the setting does not preserve the source IP of the request.
* When you delete a VPC cluster, any non-persistent VPC load balancers, which are named in the `kube-<cluster_ID>-<kubernetes_lb_service_UID>` format and are automatically created by {{site.data.keyword.openshiftlong_notm}} for the Kubernetes `LoadBalancer` services in that cluster, are also automatically deleted. However, [persistent load balancers](/docs/openshift?topic=openshift-vpclb_manage#vpc_lb_persist) with unique names and VPC load balancers that you manually created in your VPC are not deleted.
* You can register up to 128 subdomains for VPC load balancer hostnames. This limit can be lifted on request by opening a [support case](/docs/get-support?topic=get-support-using-avatar).
* Subdomains that you register for VPC load balancers are limited to 130 characters or fewer.
* VPC ALBs listen on the same VPC subnets that the cluster worker nodes are allocated on unless the Kubernetes load balancer service is created with the `service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-subnets` or `service.kubernetes.io/ibm-load-balancer-cloud-provider-zone` annotations, which limit traffic to specific nodes.
    * The subnets and zones of the VPC ALB can be updated or modified after the ALB is created. If you add more zones to the cluster or update the Kubernetes load balancer service with the `service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-subnets` or `service.kubernetes.io/ibm-load-balancer-cloud-provider-zone` annotations, the VPC ALB is updated to listen on the new subnets. 
* VPC NLBs listen only on a single VPC subnet in a single zone. They cannot be configured to listen on multiple VPC subnets or to listen on multiple zones. You can specify the single subnet for an NLB to listen on with the `service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-subnets` or `service.kubernetes.io/ibm-load-balancer-cloud-provider-zone` annotations. 
    * VPC NLBs forward incoming traffic to all worker nodes in the cluster unless you restrict incoming traffic to specific worker nodes with the `service.kubernetes.io/ibm-load-balancer-cloud-provider-vpc-node-selector` or `service.kubernetes.io/ibm-load-balancer-cloud-provider-zone annotations`. To limit traffic to a specific zone, you can use these annotations to specify worker nodes in that zone. 
* Disabling load balancer NodePort allocation is not supported for VPC load balancers. 
* VPC NLBs can be set up with both UDP and TCP on the same VPC LB, but the listening port must be different.
