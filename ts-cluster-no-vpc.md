---

copyright: 
  years: 2014, 2022
lastupdated: "2022-05-06"

keywords: openshift

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# VPC: Why is no VPC available when I create a cluster in the console?
{: #ts_no_vpc}
{: support}

**Infrastructure provider**: ![VPC](../icons/vpc.svg "VPC") VPC

You try to create a VPC cluster by using the [{{site.data.keyword.openshiftlong_notm}} console](https://cloud.ibm.com/kubernetes/catalog/create){: external}.
{: tsSymptoms} 

You have an existing [VPC](https://cloud.ibm.com/vpc){: external} in your account, but when you try to select an existing **Virtual Private Cloud** to create the cluster in, you see the following error message:
```sh
No VPC is available. Create a VPC.
```
{: screen}

During cluster creation, the {{site.data.keyword.openshiftlong_notm}} console uses the API key that is set for the `default` resource group to list the VPCs that are available in your {{site.data.keyword.cloud_notm}} account.
{: tsCauses}

If no API key is set for the `default` resource group, no VPCs are listed in the {{site.data.keyword.openshiftlong_notm}} console, even if your VPC exists in a different resource group and an API key is set for that resource group.

To set an API key for the `default` resource group, use the {{site.data.keyword.openshiftlong_notm}} CLI.
{: tsResolve}

1. Log in to the command line as the account owner. If you want a different user than the account owner to set the API key, first [ensure that the API key owner has the correct permissions](/docs/openshift?topic=openshift-access-creds#owner_permissions).
    ```sh
    ibmcloud login [--sso]
    ```
    {: pre}

2. Target the `default` resource group.
    ```sh
    ibmcloud target -g default
    ```
    {: pre}

3. Set the API key for the region and resource group.
    ```sh
    ibmcloud oc api-key reset --region <region>
    ```
    {: pre}

4. In the [{{site.data.keyword.openshiftlong_notm}} console](https://cloud.ibm.com/kubernetes/catalog/create){: external}, click **Refresh VPCs**. Your available VPCs are now listed in a drop-down menu.



