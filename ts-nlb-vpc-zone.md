---

copyright: 
  years: 2024, 2024
lastupdated: "2024-09-03"


keywords: openshift, kubernetes, help, network, connectivity, vpc nlb

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# VPC Clusters: My VPC NLB has a zone error and does not update
{: #ts-nlb-vpc-zone}


Your VPC NLB does not update when worker nodes are added or removed from your cluster. Additionally, you see an error similar to the following:
{: tsSymptoms}

```sh
The load balancer was created in zone <zone>. This setting can not be changed.
```
{: screen}

You included the `service.kubernetes.io/ibm-load-balancer-cloud-provider-zone` annotation in your VPC NLB configuration and then later changed the specified zone. Changing the annotation to a different zone creates an error and prevents the VPC NLB from updating when worker nodes are added or removed from the cluster. This might cause all network traffic through the load balancer to fail if all of the cluster's worker nodes are upgraded and refreshed simultaneously. 
{: tsCauses}

You can change the zone specified by the `service.kubernetes.io/ibm-load-balancer-cloud-provider-zone` annotation for VPC ALBs, but not for VPC NLBs. 
{: note}

Change the `service.kubernetes.io/ibm-load-balancer-cloud-provider-zone` annotation back to the original zone that was specified when you created the load balancer. If you still need to change the NLB's zone, you must delete, update, and reapply the corresponding Kubernetes `LoadBalancer` service. For more information, see [Changing a load balancer's subnet or zone](/docs/openshift?topic=openshift-vpclb_manage#lbaas_change_subnets). 
{: tsRemedy}
