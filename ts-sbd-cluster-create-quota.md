---

copyright: 
  years: 2024, 2024
lastupdated: "2024-11-25"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, secure by default, {{site.data.keyword.openshiftlong_notm}}, outbound traffic protection, cluster create, quotas, limitations, rules, security groups

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# When I create a VPC cluster, my worker nodes are stuck in `Pending security group creation`
{: #ts-sbd-cluster-create-quota}
{: support}

[Virtual Private Cloud]{: tag-vpc}
[4.15 and later]{: tag-red}


After you create a VPC cluster, your worker nodes are stuck in the `Provision_pending` state with the message `Pending security group creation` .
{: tsSymptoms}

Example worker node. 
```sh
cluster-default-00000  -     bx2.4x16   provision_pending   Pending security group creation   us-south-2   -
```
{: screen}


Your VPC has reached the limit of clusters or security groups allowed per VPC. For more information, see the [VPC security group quotas](/docs/vpc?topic=vpc-quotas#security-group-quotas).
{: tsCauses}

Review the quota limitations that might cause the issue. 

Cluster limit
:   Because of security group limitations, a single VPC can have a maximum number of 15 clusters. This is a hard limit with no exceptions. 

Security group limit
:   Every time a  VPC cluster is created, additional security groups are automatically created for the cluster and its worker nodes. However, there is a limited number of security groups that can exist in a VPC. If this limit is reached, additional security groups cannot be created for the cluster or worker nodes that you provisioned. 

Review the logging messages from the `network-microservice` to see details on which quota was exceeded.
{: tsResolve}

After reviewing the logging messages, complete the steps in the following sections for the quota you exceeded.


## If you have reached the number of clusters allowed per VPC
{: #quota-cluster-max}

If you have already reached the 15 cluster maximum for your VPC, the worker nodes on any additional cluster you provision remain in the `pending` state. There are no exceptions to this quota. You can either [delete a cluster](/docs/containers?topic=containers-remove) from your VPC, or [create a new VPC](/docs/vpc?topic=vpc-creating-vpc-resources-with-cli-and-api&interface=cli#create-a-vpc-cli) where you can provision additional clusters. 

If you choose to delete a cluster from your existing VPC, [refresh the cluster master](/docs/containers?topic=containers-kubernetes-service-cli#cs_apiserver_refresh) to continue provisioning your worker nodes. 

    ```sh
    ibmcloud oc cluster master refresh -c <cluster_name_or_ID>
    ```
    {: pre}


## If you have reached the number of security groups allowed per VPC
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

1. If you can't delete the security groups, any new clusters must be created in a different VPC. Alternatively, a ticket can be opened against the account to request a quota increase. Open a [support case](/docs/account?topic=account-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.
