---

copyright: 
  years: 2022, 2022
lastupdated: "2022-10-07"

keywords: openshift

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why am I running out of SNAT ports for egress connections from pods in my cluster?
{: #ts-network-snat-125}
{: support}

As of {{site.data.keyword.openshiftlong_notm}} 4.12 the source Network Address Translation (NAT) port range has change to `32768 - 65535`, where previously it was `1024 - 65535`. This change was made to resolve possible issues where the following scenarios might occur.
{: tsSymptoms}

- An SNAT port is chosen in a VPC cluster that conflicts with a NodePort of a LoadBalancer of type NLB. In this case, that egress connection fails.
- An SNAT port is chosen for a long running egress connection in the NodePort range of 30,000 - 32,767 that a cluster service later wants to use for a NodePort. In this case, that cluster service won't get traffic on that NodePort until the connection using that SNAT port is finished and has been closed.
- An SNAT port is chosen for a long running egress connection that a Linux service or `hostPort` pod port or `hostNetwork` pod port later wants to use. In that case, that service or pod won't start or work until the connection that is using that SNAT port is finished and has been closed.

Usually, limiting this port range is fine. However, if you are running a highly scalable application in pod-network pods, where on a single worker you have either of the following cases.
{: tsCauses}

- Over 30,000 egress connections to destinations other than pods or nodes in the cluster open at once.
- 30,000 egress connections are being opened within a few minutes of each other.



It might be possible that the 32768 - 65535 range isn't large enough. Two possible solutions to this are the following options.
{: tsResolve}

- Add more nodes and have at least one pod per node that make all these egress connections so that each node needs less than 30,000 SNAT ports. This is the preferred solution
- Explicitly set the pod `natPortRange` in Calico to a larger range. Note that this might cause the occasional port conflicts listed previously if you use VPC NLBs or add NodePort services or `hostPort` pods that use specific hardcoded ports

If you do want to set this port range, you must download the `calicoctl` binary, set the `KUBECONFIG` environment variable for the cluster, and run the following command where `LOWER_RANGE_LIMIT` is between `1025` and `32767`. 

This change takes effect immediately, and if you do this prior to updating your cluster master to 1.25 then the update doesn't overwrite what you set.

```sh
calicoctl patch felixconfiguration default --patch '{"spec":{"natPortRange": "LOWER_RANGE_LIMIT:65535"}}' 
```
{: pre}

