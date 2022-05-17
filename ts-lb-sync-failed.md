---

copyright: 
  years: 2014, 2022
lastupdated: "2022-05-17"

keywords: openshift

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why do I see `SyncLoadBalancerFailed` errors when creating a VPC cluster?
{: #ts-loadbalancer-sync-failed}
{: support}

When setting up load balancing on my VPC cluster, I see an error message similar to the following.
{: tsSymptoms}

```sh
Warning  CreatingCloudLoadBalancerFailed  55s                ibm-cloud-provider  Error on cloud load balancer kube-<CLUSTERID>-<SERVICE_UUID> for service <NAMESPACE>/<SERVICE_NAME> with UID <SERVICE_UUID>: Failed ensuring LoadBalancer: FindLoadBalancer failed: FindLoadBalancer failed: An error occurred while performing the 'authenticate' step: 400 Bad Request [{"incidentID":"XXX","code":"XXX","description":"Error message from IAM: '401 Unauthorized. Transaction-Id: XXX Details: {\"errorCode\":\"BXNIM0430E\",\"errorMessage\":\"User login from given IP address is not permitted.\",\"errorDetails\":\"The user has configured IP address restriction for login. The given IP address 'XXXX' is not contained in the list of allowed IP addresses.\",\"context\":...,"type":"Authentication"}]
Warning  SyncLoadBalancerFailed           55s                service-controller  Error syncing load balancer: failed to ensure load balancer: Error on cloud load balancer kube-<CLUSTERID>-<SERVICE_UUID> for service <NAMESPACE>/<SERVICE_NAME> with UID <SERVICE_UUID>:: Failed ensuring LoadBalancer: FindLoadBalancer failed: FindLoadBalancer failed: An error occurred while performing the 'authenticate' step: 400 Bad Request [{"incidentID":"XXX","code":"XXX","description":"Error message from IAM: '401 Unauthorized. Transaction-Id: XXX Details: {\"errorCode\":\"BXNIM0430E\",\"errorMessage\":\"User login from given IP address is not permitted.\",\"errorDetails\":\"The user has configured IP address restriction for login. The given IP address 'XXX' is not contained in the list of allowed IP addresses.\",\"context\":...,"type":"Authentication"}]
```
{: screen}

This error occurs when your IAM allowlist doesn't allow the necessary communication to control plane IPs.
{: tsCauses}

To resolve this issue, add the control plane IPs for the region where your cluster is located to your IAM allowlist.
{: tsResolve}

For a list of control plane IPs by region, see the `IBM/kube-samples` [repo](https://github.com/IBM-Cloud/kube-samples/tree/master/control-plane-ips){: external}


