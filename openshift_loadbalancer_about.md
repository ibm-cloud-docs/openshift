---

copyright:
  years: 2014, 2019
lastupdated: "2019-12-03"

keywords: openshift, roks, rhos, rhoks, lb2.0, nlb

subcollection: openshift

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:preview: .preview} 

# About network load balancers (NLBs)
{: #loadbalancer-about}

When you create a standard cluster, {{site.data.keyword.openshiftlong}} automatically provisions a portable public subnet and a portable private subnet.
{: shortdesc}

* The portable public subnet provides 5 usable IP addresses. 1 portable public IP address is used by the default [public Ingress ALB](/docs/openshift?topic=openshift-ingress). The remaining 4 portable public IP addresses can be used to expose single apps to the internet by creating public network load balancer services, or NLBs.
* The portable private subnet provides 5 usable IP addresses. 1 portable private IP address is used by the default [private Ingress ALB](/docs/openshift?topic=openshift-ingress#private_ingress). The remaining 4 portable private IP addresses can be used to expose single apps to a private network by creating private load balancer services, or NLBs.

To make an app accessible through both a portable public and a portable private IP address, you must create both a public NLB and a private NLB. Portable public and private IP addresses are static floating IPs and do not change when a worker node is removed. If the worker node that the NLB IP address is on is removed, a Keepalived daemon that constantly monitors the IP automatically moves the IP to another worker node. You can assign any port to your NLB. The NLB serves as the external entry point for incoming requests for the app. To access the NLB from the internet, you can use the public IP address of your NLB and the assigned port in the format `<IP_address>:<port>`. You can also create DNS entries for NLBs by registering the NLB IP addresses with subdomains.

When you expose an app with an NLB service, your app is automatically made available over the service's NodePorts too. [NodePorts](/docs/openshift?topic=openshift-nodeport) are accessible on every public and private IP address of every worker node within the cluster. To block traffic to NodePorts while you are using an NLB, see [Controlling inbound traffic to network load balancer (NLB) or NodePort services](/docs/openshift?topic=openshift-network_policies#block_ingress).

<br />


## Components and architecture of an NLB 1.0
{: #v1_planning}

The TCP/UDP network load balancer (NLB) 1.0 uses Iptables, a Linux kernel feature to load balance requests across an app's pods.
{: shortdesc}

### Traffic flow in a single-zone cluster
{: #v1_single}

The following diagram shows how an NLB 1.0 directs communication from the internet to an app in a single-zone cluster.
{: shortdesc}

<img src="images/cs_loadbalancer_planning.png" alt="Expose an app in a single-zone cluster by using an NLB 1.0" width="550" style="width:550px; border-style: none"/>

1. A request to your app uses the public IP address of your NLB and the assigned port on the worker node. Note that if you [create a DNS subdomain](/docs/openshift?topic=openshift-loadbalancer_hostname) for your NLB, users can access your app through the NLB's subdomain instead. A DNS system service resolves the subdomain to the portable public IP address of the NLB.

2. The NLB receives the request and forwards it to the private IP address of the app pod over the private network. The source IP address of the request package is changed to the public IP address of the worker node where the NLB pod runs. If multiple app instances are deployed in the cluster, the NLB routes the requests between the app pods.

3. When the app returns a response packet, it uses the IP address of the worker node where the NLB that forwarded the client request exists. The NLB then sends the response packet to the client.

### Traffic flow in a multizone cluster
{: #v1_multi}

The following diagram shows how a network load balancer (NLB) 1.0 directs communication from the internet to an app in a multizone cluster.
{: shortdesc}

<img src="images/cs_loadbalancer_planning_multizone.png" alt="Use an NLB 1.0 to load balance apps in a multizone cluster" width="600" style="width:600px; border-style: none"/>

1. A request to your app uses the [DNS subdomain](/docs/openshift?topic=openshift-loadbalancer_hostname) for your NLBs. You can also access the NLB in each zone by using its public IP address and port on the worker node. Note that by default, each NLB 1.0 is set up in one zone only. To achieve high availability, you must deploy an NLB 1.0 in every zone where you have app instances.

2. A DNS system service resolves the subdomain to the portable public IP address of one of the NLBs and its assigned port on the worker node. Requests are handled by the NLBs in various zones in a round-robin cycle.

3. The NLB receives the request and forwards it to the private IP address of the app pod over the private network. The source IP address of the request package is changed to the public IP address of the worker node where the NLB pod runs. Each NLB routes requests to the app instances in its own zone and to app instances in other zones. Additionally, if multiple app instances are deployed in one zone, the NLB routes the requests between the app pods in the zone.

4. When the app returns a response packet, it uses the IP address of the worker node where the NLB that forwarded the client request exists. The NLB then sends the response packet to the client.



</staging components>
