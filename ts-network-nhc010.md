---

copyright: 
  years: 2025, 2026
lastupdated: "2026-09-02"

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


Troubleshoot network health check error NHC010.
{: shortdesc}

When you check the status of your cluster's health by running the `ibmcloud oc cluster health issues --cluster <CLUSTER_ID>`, you see an error similar to the following example.
{: tsSymptoms}

```sh
ID       Component   Severity   Description
NHC010   Network     Error      Exceeded security group rules related quota.
```
{: screen}

IBM Cloud VPC infrastructure enforces a limit of 100 security groups per VPC. Each cluster creation adds security groups, and this limit is reached around 33 clusters. 25 clusters per VPC is the recommended maximum. If this [limit](/docs/vpc?topic=vpc-quotas#service-limits-for-vpc-services){: external} is exceeded, it can prevent your cluster from creating or updating required security group rules, meaning you cannot create another cluster.
{: tsCauses}

Review and adjust your cluster's security group configuration.
{: tsResolve}

1. There are multiple security groups associated with a VPC cluster that need to be checked. One example is a shared security group named in the format `kube-vpegw-<VPC_ID>`. Each cluster creation adds security groups to the VPC, and a VPC supports a maximum of 100 security groups. Once this limit is reached, you cannot create more clusters. To check the current number of security groups in your VPC, run:
    ```sh
    ibmcloud is security-groups --vpc <VPC_ID> --output json | jq 'length'
    ```
    {: pre}

2. If the count is at or near 100, you must free up security groups before you can create more clusters. To resolve this:

    - Delete unused clusters in the VPC to remove their associated security groups.
    - Or [create a new VPC](/docs/vpc?topic=vpc-creating-vpc-resources-with-cli-and-api&interface=cli#create-a-vpc-cli) where you can provision additional clusters.

3. After making adjustments, wait a few minutes and check if the warning clears.

4. If the issue persists, contact support for further assistance. Open a [support case](/docs/support?topic=support-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.
