---

copyright: 
  years: 2025, 2025
lastupdated: "2025-08-11"

keywords: nhc009, IAM token exchange failed

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why does the Network status show an `NHC009` error?
{: #ts-network-nhc009}
{: troubleshoot}
{: support}

[Virtual Private Cloud]{: tag-vpc}

When you check the status of your cluster's health by running the `ibmcloud oc cluster health issues --cluster <CLUSTER_ID>`, you see an error similar to the following example.
{: tsSymptoms}

```sh
ID       Component   Severity   Description
NHC009   Network     Error      The IAM token exchange request failed.
```
{: screen}

VPC operations rely on IAM API keys for authentication. If the used API key is invalid, expired, or disabled, that can lead to this error.
{: tsCauses}

Review and update your IBM Cloud API key used for the IBM Cloud Kubernetes Service.
{: tsResolve}

1. Find out which API key is used. Check the resource group of your cluster by running the following command:
    ```sh
    ibmcloud ks cluster get --cluster <Cluster_ID>
    ```
    {: pre}

2. To find the associated API key run the following command and look for the associated API key for IBM Cloud Kubernetes Service for resource group, and save the ApiKey ID for later:
    ```sh
    ibmcloud iam api-key --uuid containers-kubernetes-key
    ```
    {: pre}

3. Verify whether the key is disabled or not by running:
    ```sh
    ibmcloud iam api-key --activity <ApiKey_ID>
    ```
    {: pre}

4. If necessary, you can reset the API key used for the IBM Cloud Kubernetes Service by running:
    ```sh
    ibmcloud ks api-key reset --region <region>
    ```
    {: pre}

5. Or if the API key disabled, enable it by running:
    ```sh
    ibmcloud iam api-key-enable <ApiKey_ID>
    ```
    {: pre}

6. For detailed steps, see [Setting the cluster credentials](/docs/openshift?topic=openshift-access-creds){: external} and [Managing IAM access, API keys, trusted profiles, service IDs, and access groups](/docs/cli?topic=cli-ibmcloud_commands_iam){: external}.

7. After fixing the API key issue you have to wait maximum 30 minutes to see if the warning is resolved.

8. If the issue persists, contact support for further assistance. Open a [support case](/docs/account?topic=account-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.
