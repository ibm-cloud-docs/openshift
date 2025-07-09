---

copyright: 
  years: 2025, 2025
lastupdated: "2025-07-09"

keywords: , nhc010, exceeded security group rules quota

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why does the Network status show an `NHC010` error?
{: #ts-network-nhc010}
{: troubleshoot}
{: support}

[Virtual Private Cloud]{: tag-vpc}

When you check the status of your cluster's network components by running the `ibmcloud ocks cluster health issues --cluster <CLUSTER_ID>`, you see an error similar to the following example.
{: tsSymptoms}

```sh
ID       Component   Severity   Description
NHC010   Network     Error      Exceeded security group rules related quota.
```
{: screen}

IBM Cloud enforces a limit of 15 remote security group rules per security group in production environments. If this limit is exceeded, it can prevent your cluster from creating or updating required security group rules. This might also block adding more resources, such as worker nodes.
{: tsCauses}

Review and adjust your cluster's security group rules.
{: tsResolve}

1. Each cluster has a dedicated security group named `kube-<CLUSTER_ID>`. First, retrieve your cluster's security group ID (SECURITY_GROUP_ID) by running:
    ```sh
    ibmcloud is security-groups <VPC_ID> --output json | jq -r '.[] | select(.name=="kube-<CLUSTER_ID>") | .id'
    ```
    {: pre}

2. Count how many remote security group rules are associated with this group:
    ```sh
    ibmcloud is security-group-rules <SECURITY_GROUP_ID> | grep -c <CLUSTER_ID>
    ```
    {: pre}

3. If the count reaches **15**, you are at the quota limit. To resolve this:

    - Reduce the number of individual rules by combining them where possible, for example by using CIDR ranges.
    - Remove duplicate rules that point to the same remote group or IP addresses.
    - Review and clean up any unnecessary rules.

4. For IBM Cloud enforced limits, see [VPC Security Group Rule Limits & Quotas](/docs/vpc?topic=vpc-quotas){: external}.

5. For general best practices, see the [Security Group Guidelines](/docs/security-groups?topic=security-groups-security-groups-guidelines){: external}.

6. For command references, see the [Security Group Rule CLI Reference](/docs/vpc?topic=vpc-vpc-reference#security-group-rule-view){: external}.

7. After making adjustments, wait a few minutes and check if the warning clears.

8. If the issue persists, contact support for further assistance. Open a [support case](/docs/account?topic=account-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.
