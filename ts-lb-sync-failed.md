---

copyright: 
  years: 2014, 2026
lastupdated: "2026-09-30"


keywords: openshift

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}



# Why do I see `SyncLoadBalancerFailed` errors when creating a VPC cluster?
{: #ts-loadbalancer-sync-failed}
{: support}


Troubleshoot issues when network load balancer (NLB) synchronization fails in your cluster.
{: shortdesc}

When setting up load balancing on my VPC cluster, I see an error message similar to the following example.
{: tsSymptoms}

```sh
Warning  CreatingCloudLoadBalancerFailed  55s                ibm-cloud-provider  Error on cloud load balancer kube-<CLUSTERID>-<SERVICE_UUID> for service <NAMESPACE>/<SERVICE_NAME> with UID <SERVICE_UUID>: Failed ensuring LoadBalancer: FindLoadBalancer failed: FindLoadBalancer failed: An error occurred while performing the 'authenticate' step: 400 Bad Request [{"incidentID":"XXX","code":"XXX","description":"Error message from IAM: '401 Unauthorized. Transaction-Id: XXX Details: {\"errorCode\":\"BXNIM0430E\",\"errorMessage\":\"User login from given IP address is not permitted.\",\"errorDetails\":\"The user has configured IP address restriction for login. The given IP address 'XXXX' is not contained in the list of allowed IP addresses.\",\"context\":...,"type":"Authentication"}]
Warning  SyncLoadBalancerFailed           55s                service-controller  Error syncing load balancer: failed to ensure load balancer: Error on cloud load balancer kube-<CLUSTERID>-<SERVICE_UUID> for service <NAMESPACE>/<SERVICE_NAME> with UID <SERVICE_UUID>:: Failed ensuring LoadBalancer: FindLoadBalancer failed: FindLoadBalancer failed: An error occurred while performing the 'authenticate' step: 400 Bad Request [{"incidentID":"XXX","code":"XXX","description":"Error message from IAM: '401 Unauthorized. Transaction-Id: XXX Details: {\"errorCode\":\"BXNIM0430E\",\"errorMessage\":\"User login from given IP address is not permitted.\",\"errorDetails\":\"The user has configured IP address restriction for login. The given IP address 'XXX' is not contained in the list of allowed IP addresses.\",\"context\":...,"type":"Authentication"}]
```
{: screen}

This error occurs when your IAM allowlist doesn't allow the necessary communication to control plane IPs.
{: tsCauses}

To resolve this issue, [add the Kubernetes Service network zone to your IAM allowlist](/docs/openshift?topic=openshift-vpc-firewall#iam_firewall).
{: tsResolve}
