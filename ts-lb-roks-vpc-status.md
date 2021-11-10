---

copyright:
  years: 2014, 2021
lastupdated: "2021-11-10"

keywords: openshift

subcollection: openshift
content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# VPC clusters: Why do I see VPC load balancer health status failures?
{: #vpc_lb_healthcheck}

**Supported infrastructure provider and versions**:
* ![VPC infrastructure provider icon.](images/icon-vpc-2.svg) VPC
* <img src="images/icon-version-43.png" alt="Version 4 icon" width="30" style="width:30px; border-style: none"/> {{site.data.keyword.openshiftshort}} version 4 clusters


In the [Load balancers for VPC dashboard](https://cloud.ibm.com/vpc-ext/network/loadBalancers){: external}, you view the details of the VPC load balancer that exposes your cluster's router.
{: tsSymptoms}

Although traffic to your apps is flowing correctly in your cluster, the **Health status** of the VPC load balancer shows that at most 2 instances (worker nodes) are **Passing**, while all other instances are **Failing**. For example, if you have 4 worker nodes in your cluster, the health status shows `2/4`.


In VPC clusters, a VPC load balancer that exposes the router is automatically created outside of your cluster. In the configuration for the load balancer, `externalTrafficPolicy` is set to `Local`, which offers better routing performance than `Cluster`.
{: tsCauses}

This `externalTrafficPolicy: Local` setting indicates that when the VPC load balancer receives a request to your app service's node port, the load balancer forwards the traffic only to router pods that are also on the same worker node as the app service's node port.

By default in the OpenShift Container Platform Ingress controller, only 2 router pods are deployed to your cluster, so only 2 worker nodes have router pods. Because the VPC load balancer forwards traffic only to worker nodes that contain router pods, the load balancer's health check only reports the 2 worker nodes that have the router pods as **Passing**, and the other worker nodes as **Failing**. For this reason, the failures are expected, and do not indicate that your VPC load balancer is unable to forward traffic to your cluster.







