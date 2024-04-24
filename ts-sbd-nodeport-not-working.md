---

copyright: 
  years: 2024, 2024
lastupdated: "2024-04-24"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, secure by default, node port not working, {{site.data.keyword.openshiftlong_notm}}, outbound traffic protection

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# When I update my cluster to 4.15 or later, my nodeport app no longer works
{: #ts-sbd-nodeport-not-working}
{: support}

[Virtual Private Cloud]{: tag-vpc}
[4.15 and later]{: tag-red}

Requests sent to your nodeport service fail with a timeout error.
{: tsSymptoms}



{{site.data.keyword.openshiftlong_notm}} managed load balancer services (ALB, NLB, sdNLB) dynamically adjust the security group rules as they are added, deleted or updated. Rules are also maintained to allow traffic through the nodeports opened by these services. Whenever possible, it is recommended to use {{site.data.keyword.openshiftlong_notm}} managed load balancer services.

If you don't use {{site.data.keyword.openshiftlong_notm}} managed load balancer services, then any unmanaged node port services and the associated security group rules to allow traffic through these node ports are your responsibility.
{: tsCauses}

Update the security group rules for your node port service.
{: tsResolve}

1. Review the [VPC security group quotas](/docs/vpc?topic=vpc-quotas#security-group-quotas).
1. Identify the node ports that are opened by your node port service.
1. For each node port opened, create a security group rule.
    ```sh
    ibmcloud is sg-rulec kube-<cluster ID> inbound <tcp/udp> --port-min <nodeport> --port-max <nodeport> --remote 0.0.0.0/0
    ```
    {: pre}

There are quota limitations on the number of rules allowed per security group. If adding the custom nodeport rule exceeds this quota the rule is not added. In this case, consider using an {{site.data.keyword.openshiftlong_notm}} managed load balancer service or modifying the `port-min` or `port-max` settings on your rule(s) to use a nodeport range.
{: note}


