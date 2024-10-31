---

copyright: 
  years: 2024, 2024
lastupdated: "2024-10-30"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, subnet, detach, specified subnet, infrastructure operation failed

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# Why do I get an `infrastructure operation failed` error when creating a VPC cluster?
{: #ts-resource-group-permissions}
{: support}

When you try to create a VPC cluster, you see an error message similar to the following.
{: tsSymptoms}

```sh
Unable to create cluster. The 'vpc-gen2' infrastructure operation failed with the message: the provided token is not authorized to view the specified subnet (ID:XXXX) in this account
```
{: screen}

The API key of the user or service ID that is trying to create the cluster does not have the required IAM permissions to view VPC subnets in your account.
{: tsCauses}

A common scenario for this error is having your VPC subnets in different resource groups from the cluster. Make sure that the API key that was used to create the cluster has at least **Viewer** access to those subnets.


Complete the following steps to resolve the issue.
{: tsResolve}

1. Review the steps in the [Preparing you account to create clusters](/docs/openshift?topic=openshift-clusters) documentation. 

1. Review the details of the API key that was used to create the cluster.
    ```sh
    ibmcloud oc api-key info
    ```
    {: pre}

    Example output
    ```sh
    ibmcloud oc api-key info -c CLUSTER
    Getting information about the API key owner for cluster CLUSTER...
    OK
    Name                Email
    User 2   usertwo@us.ibm.com
    ```
    {: screen}

1. Add the **Viewer** access role for the VPC subnet mentioned in the error message or for all subnets in the VPC.

1. Retry the cluster creation steps.

1. If the issue persists, contact support. Open a [support case](/docs/account?topic=account-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.
