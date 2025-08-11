
---

copyright: 
  years: 2025, 2025
lastupdated: "2025-08-11"

keywords: nhc010, exceeded security group rules quota

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why does the Network status show an `NHC010` error?
{: #ts-network-nhc010}
{: troubleshoot}
{: support}

[Virtual Private Cloud]{: tag-vpc}

When you check the status of your cluster's health by running the `ibmcloud oc cluster health issues --cluster <CLUSTER_ID>`, you see an error similar to the following example.
{: tsSymptoms}

```sh
ID       Component   Severity   Description
NHC010   Network     Error      Exceeded security group rules related quota.
```
{: screen}

IBM Cloud VPC infrastructure enforces limits for security group rules per security group in production environments. If this [limit](/docs/vpc?topic=vpc-quotas#service-limits-for-vpc-services){: external} is exceeded, it can prevent your cluster from creating or updating required security group rules. So it means for example you cannot create another cluster.
{: tsCauses}

Review and adjust your cluster's security group rules.
{: tsResolve}

1. There are multiple security groups associated with a VPC cluster that need to be checked. One example is a shared security group named in the format `kube-vpegw-<VPC_ID>`. Each associated security group typically includes the CLUSTER_ID in its name, making it easier to identify which cluster it belongs to. The shared security group has remote security group rules referencing these associated groups, and it cannot have more than 15 such remote rules. Each cluster in the same VPC has an entry, and once it reaches 15, you cannot create more clusters. To check the number of remote rules, first retrieve the security group ID (SECURITY_GROUP_ID) for the shared security group by running:
    ```sh
    ibmcloud is security-groups <VPC_ID> --output json | jq -r '.[] | select(.name=="kube-vpegw-<VPC_ID>") | .id'
    ```
    {: pre}

2. Count how many remote security group rules are associated with this group:
    ```sh
    ibmcloud is security-group-rules <SECURITY_GROUP_ID> | grep -c <CLUSTER_ID>
    ```
    {: pre}

3. If the count reaches the limit. To resolve this:

    - Use different VPC or cleanup unused clusters in the VPC.
    - Or if you have added custom remote rules earlier, than you can review them:
      - Reduce the number of custom individual rules.
      - Remove duplicate custom rules that point to the same remote group or IP addresses.
      - Review and clean up any unnecessary custom rules.

4. For IBM Cloud enforced limits, see [VPC Security Group Rule Limits & Quotas](/docs/vpc?topic=vpc-quotas){: external}.

5. For general best practices, see the [Security Group Guidelines](/docs/security-groups?topic=security-groups-security-groups-guidelines){: external}.

6. For command references, see the [Security Group Rule CLI Reference](/docs/vpc?topic=vpc-vpc-reference#security-group-rule-view){: external}.

7. After making adjustments, wait a few minutes and check if the warning clears.

8. If the issue persists, contact support for further assistance. Open a [support case](/docs/account?topic=account-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.
