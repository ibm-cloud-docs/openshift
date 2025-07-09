---

copyright: 
  years: 2025, 2025
lastupdated: "2025-07-09"

keywords: , nhc011, exceeded security group quota

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why does the Network status show an `NHC011` error?
{: #ts-network-nhc011}
{: troubleshoot}
{: support}

[Virtual Private Cloud]{: tag-vpc}

When you check the status of your cluster's network components by running the `ibmcloud ocks cluster health issues --cluster <CLUSTER_ID>`, you see an error similar to the following example.
{: tsSymptoms}

```sh
ID       Component   Severity   Description
NHC011   Network     Error      Exceeded security group related quota.
```
{: screen}

This error occurs when your VPC (Virtual Private Cloud) has reached the quota limit for security groups (100 security groups per VPC). Each Kubernetes cluster and its worker nodes require dedicated security groups, and exceeding this quota prevents additional provisioning.
{: tsCauses}

Review and reduce the number of security groups in your VPC.
{: tsResolve}

1. Check the current number of security groups in your VPC by running:
    ```sh
    ibmcloud is sgs | grep <vpc-name> -c
    ```
    {: pre}

2. If the count is at or exceeds the quota, clean up unused security groups. For example:
    ```sh
    ibmcloud is security-group-delete <group-1> <group-2> ... <group-n> --vpc <VPC-ID>
    ```
    {: pre}

3. Alternatively, consider deleting unused Kubernetes clusters to free up associated security groups.

4. After cleanup, trigger a master refresh to ensure required security groups can be re-created:
    ```sh
    ibmcloud ks cluster master refresh -c <clusterID>
    ```
    {: pre}

5. For IBM Cloud limits, see the [VPC Security Group Limits & Quotas](/docs/vpc?topic=vpc-quotas){: external}.

6. For command references, see the [Security Group CLI Reference](/docs/vpc?topic=vpc-vpc-reference#security-groups-cli-ref){: external}.

7. Wait a few minutes, then recheck your cluster status.

8. If the issue persists, contact support for further assistance. Open a [support case](/docs/account?topic=account-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.
