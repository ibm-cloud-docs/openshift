---

copyright: 
  years: 2025, 2025
lastupdated: "2025-10-02"


keywords: openshift, kubernetes, help, network, private path nlb, ppnlb

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# Why does my Private Path NLB contain a `hostname.invalid` error?
{: #ts-ppnlb-hostname}
{: support}



When describing your LoadBalancer by using the `oc describe svc SERVICENAME -n NAMESPACE` command, you see an error message similar to the following.
{: tsSymptoms}

```sh
Error on cloud load balancer prod-sat1-ppnlb for service openshift-ingress/router-default-ppnlb with UID c89cde55-777f-4d99-aacf-09108d90fa9c: Service and associated VPC load balancer do not match: Service external IPs:, VPC load balancer IPs:XX.XX.XX.XX,XX.XX.XX.XX,XX.XX.XX.XX,XX.XX.XX.XX
```
{: screen}

You also see the LoadBalancer Ingress field contains `hostname.invalid`.

```yaml
LoadBalancer Ingress: hostname.invalid
```
{: screen}


The issue is caused by a mismatch between the Kubernetes service configuration and the LoadBalancer. This is a known issue in versions prior to `4.16.40_1567_openshift`. The affected PPNLB was created before the rollout of the fix included in `4.16.40_1567_openshift`.
{: tsCauses}


Recreate your PPNLB to resolve the issue.
{: tsResolve}


1. Delete all associated resources linked to the service.
1. Delete and recreate the PPNLB service.
1. Verify that `hostname.invalid` no longer appears in the LoadBalancer Ingress field and that no warnings are present in the **Events** section when you describe the service.
1. If the issue persists, contact support. Open a [support case](/docs/account?topic=account-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.


