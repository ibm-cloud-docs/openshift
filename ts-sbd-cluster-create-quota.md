---

copyright: 
  years: 2024, 2024
lastupdated: "2024-05-29"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, secure by default, {{site.data.keyword.openshiftlong_notm}}, outbound traffic protection, cluster create, quotas, limitations, rules, security groups

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# When I try to create a version 4.15 cluster, I see a VPC quota error
{: #ts-sbd-cluster-create-quota}
{: support}

[Virtual Private Cloud]{: tag-vpc}
[4.15 and later]{: tag-red}


Cluster creation fails due to security group quota enforcement. You see an error message similar to one of the following.
{: tsSymptoms}


Example message where the number of remote rules per security group was exceeded.

```txt
Exceeded limit of unique remote rules per security group (the limit is 15 unique remote rules per security group).\n\nAdding a rule would exceed the limit of unique remote rules per security group. Consider creating another security group.","code":"ErrorSecurityGroupRuleOverQuota","wrapped":["over_quota: Exceeded limit of unique remote rules per security group (the limit is 15 unique remote rules per security group).\n\nAdding a rule would exceed the limit of unique remote rules per security group. Consider creating another security group. (400)","over_quota: Exceeded limit of unique remote rules per security group (the limit is 15 unique remote rules per security group).\n\nAdding a rule would exceed the limit of unique remote rules per security group. Consider creating another security group. - https://cloud.ibm.com/docs/vpc?topic=vpc-quotas","80ccf38c1b8e06cc9892762f80eaca0d"],"user_error":{"code":"P4050","description":"The '{{.Provider}}' infrastructure operation failed with the message: {{.Message}}","type":"BadRequest","terseDescription":"'{{.Provider}}' infrastructure exception: {{.Message}}","rc":400},"vars":{"Message":"Exceeded limit of unique remote rules per security group (the limit is 15 unique remote rules per security group).\n\nAdding a rule would exceed the limit of unique remote rules per security group. Consider creating another security group.","Provider":"vpc-gen2"}}}}
```
{: pre}

Example error message where the number of security groups in a VPC was exceeded.

```txt
Creating a new security group will put the user over quota. Allocated: 100, Requested: 1, Quota: 100","code":"ErrorSecurityGroupOverQuota","wrapped":["over_quota: Creating a new security group will put the user over quota. Allocated: 100, Requested: 1, Quota: 100 (400)","over_quota: Creating a new security group will put the user over quota. Allocated: 100, Requested: 1, Quota: 100 - https://cloud.ibm.com/docs/vpc?topic=vpc-quotas","e29df63c7eb284123750fab554863858"],"user_error":{"code":"P4050","description":"The '{{.Provider}}' infrastructure operation failed with the message: {{.Message}}","type":"BadRequest","terseDescription":"'{{.Provider}}' infrastructure exception: {{.Message}}","rc":400},"vars":{"Message":"Creating a new security group will put the user over quota. Allocated: 100, Requested: 1, Quota: 100","Provider":"vpc-gen2"}
```
{: pre}


Another indication of a quota error is that your worker nodes are stuck in the `Provision_pending` state with the message `Pending security group creation`.
```sh
cluster-default-00000  -     bx2.4x16   provision_pending   Pending security group creation   us-south-2   -
```
{: screen}


There are a number of different quotas associated with VPC clusters.
{: tsCauses}

This includes quotas for security groups, such as the following. 
- The number of security groups allowed per VPC.
- The number of rules allowed per security group.
- The number of rules between security groups per security group (Also called remote rules).

For more information, see the [VPC security group quotas](/docs/vpc?topic=vpc-quotas#security-group-quotas).

Review the logging messages from the `network-microservice` to see details on which quota was exceeded.
{: tsResolve}

After reviewing the logging messages, complete the steps in the following sections for the quota you exceeded.

## If you exceeded the number of security groups allowed per VPC
{: #quota-num-of-rules-per-vpc}

1. Review the [VPC security group quotas](/docs/vpc?topic=vpc-quotas#security-group-quotas).

1. Count the number of security groups in your VPC.
    ```sh
    ibmcloud is sgs | grep <vpc-name> -c
    ```
    {: pre}

    This number should be less than the quota while also allowing for the 3-4 security groups that need to be created as part of cluster creation.
    {: note}

    - If the shared VPE gateway security group (`kube-vpegw-VPC-ID`) does not exist, this group is created during cluster creation. Also, 3 additional security groups are created for a total of 4.
    - If the shared VPE gateway security group already exists, it is not created during cluster creation. The total number of security groups is 3.

1. Delete any security groups that are no longer needed. If you can't delete the security groups, any new clusters must be created in a different VPC.

    Deleting unused clusters in the VPC also removes the security groups created by {{site.data.keyword.openshiftlong_notm}}.
    {: note}

    ```sh
    ibmcloud is security-group-delete <group-1> <group-2> <group-3>
    ```
    {: pre}


1. Refresh the cluster master so that security group creation gets reprocessed.

    ```sh
    ibmcloud ks cluster master refresh -c <clusterID>
    ```
    {: pre}

1. If you can't delete the security groups, any new clusters must be created in a different VPC. Alternatively, a ticket can be opened against the account to request a quota increase. Open a [support case](/docs/get-support?topic=get-support-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.


## If you exceeded the number of remote rules per security group
{: #quota-num-of-remote-rules}

This failure is most likely happened when the shared VPE gateway security group (`kube-vpegw-<VPC-ID>`) was being modified. This security group contains a remote rule to every cluster in the VPC, and the number of remote rules on a security group is limited. Which means this limits the number of clusters that can be created in a VPC.

Review the [VPC security group quotas](/docs/vpc?topic=vpc-quotas#security-group-quotas). Any clusters that are no longer needed should be removed, and a master refresh can be run on the new cluster.  If clusters cannot be deleted, the new cluster must be created on a different VPC.


