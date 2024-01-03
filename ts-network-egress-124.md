---

copyright: 
  years: 2022, 2024
lastupdated: "2024-01-03"


keywords: openshift, egress, natportrange, 1.24

subcollection: openshift

content-type: troubleshoot

---


# Why am I seeing egress connection failures from pods?
{: #ts-network-egress-124}
{: support}



[Virtual Private Cloud]{: tag-vpc}  Gen 2

Egress connections from pods in your {{site.data.keyword.openshiftlong_notm}} version 4.11 are failing.
{: tsCauses}

If you have a LoadBalancer in your cluster of type NLB with the annotation `service.kubernetes.io/ibm-load-balancer-cloud-provider-enable-features: "nlb"` and are running {{site.data.keyword.openshiftlong_notm}} version 4.11 earlier, then your `pod-network` pod egress connections might infrequently chose one of the NodePorts that your NLB is using, which creates a conflict and causes that egress connection to fail.
{: tsCauses}


Update the pod natPortRange in Calico to `32768 - 65535` so it doesn't conflict with the NodePort range of `30000 - 32767`.
{: tsResolve} 

Run the following command to patch the Calico `natPortRange`. This change takes effect immediately.

```sh
calicoctl patch felixconfiguration default --patch '{"spec":{"natPortRange": "32768:65535"}}'
```
{: pre}

Check whether the egress connections for pods are successful. If the issue persists, contact support. Open a [support case](/docs/get-support?topic=get-support-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.
