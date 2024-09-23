---

copyright:
  years: 2023, 2024
lastupdated: "2024-09-23"


keywords: load balancer, health checks, vpc load balancer, health status, network

subcollection: openshift
content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why are VPC load balancer health checks failing on my worker nodes?
{: #vpc-lb-healthcheck-fail}
{: troubleshoot}
{: support}

 
When you check the Health Status section of your VPC load balancer details, the health checks for your load balancer worker nodes are failing. 
{: tsSymptoms}

To check the VPC loadbalancer health status, navigate to the [Load balancers for VPC page](https://cloud.ibm.com/infrastructure/network/loadBalancers){: external} in the console. Click on the relevant load balancer and review the details in the Health Status section.  
{: tip}

Depending on how your load balancer is configured, failing health checks might be the expected behavior and do not necessarily indicate a problem. If the `externalTrafficPolicy` setting for the load balancer service is set to `Local`, incoming traffic is delivered only to the application pod residing on the node that the traffic enters. If the load balancer tries to connect to any node that does not have an application pod, the traffic is dropped and the health check fails. This is the intended behavior for the `externalTrafficPolicy: Local` setting and ensures that the traffic is routed correctly. 
{: tsCauses}

If the load balancer service is configured with the `externalTrafficPolicy` set to `Local` and there are no service disruptions, then the health checks are functioning as intended and you do not need to take any action.
{: tsResolve}

If you are not sure how the `externalTrafficPolicy` setting is configured, run `oc get svc <loadbalancer_name> -n <namespace> -o yaml` and look for `externalTrafficPolicy` in the output. 
{: tip}
