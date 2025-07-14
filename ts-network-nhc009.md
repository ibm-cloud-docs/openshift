---

copyright: 
  years: 2025, 2025
lastupdated: "2025-07-14"

keywords: , nhc009, IAM token exchange failed

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why does the Network status show an `NHC009` error?
{: #ts-network-nhc009}
{: troubleshoot}
{: support}

[Virtual Private Cloud]{: tag-vpc}

When you check the status of your cluster's network components by running the `ibmcloud ocks cluster health issues --cluster <CLUSTER_ID>`, you see an error similar to the following example.
{: tsSymptoms}

```sh
ID       Component   Severity   Description
NHC009   Network     Error      The IAM token exchange request failed.
```
{: screen}

VPC operations rely on IAM API keys for authentication. If the used API key is invalid, expired, or disabled, that can lead to this error.
{: tsCauses}

Review and update your IAM API key.
{: tsResolve}

1. Find out which API key is used. Check the resource group of your cluster.
    ```sh
    ibmcloud ks cluster get --cluster <Cluster_ID>
    ```
    {: pre}

3. Use the resource group ID to find the associated API key.
    ```sh
    ibmcloud iam api-key --uuid containers-kubernetes-key
    ```
    {: pre}
   
5. Verify whether the key is disabled.
    ```sh
    ibmcloud iam api-key --activity <ApiKey_ID>
    ```
    {: pre}
   
7. If necessary, reset your Kubernetes.
    ```sh
    ibmcloud ks api-key reset
    ```
    {: pre}

8. Or, if the API key disabled, enable it.
    ```sh
    ibmcloud iam api-key-enable <ApiKey_ID>
    ```
    {: pre}

9. For detailed steps, see [Setting the cluster credentials](/docs/openshift?topic=openshift-access-creds){: external} and [Managing IAM access, API keys, trusted profiles, service IDs, and access groups](/docs/cli?topic=cli-ibmcloud_commands_iam){: external}.

10. Wait 30 minutes, then check if the warning is resolved.

11. If the issue persists, contact support for further assistance. Open a [support case](/docs/account?topic=account-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.
