---

copyright: 
  years: 2024, 2025
lastupdated: "2025-03-05"

keywords: license, entitlement, OCP, Cloud Pak, {{site.data.keyword.openshiftlong_notm}}

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why do I see a license or entitlement error when creating a worker pool?
{: #ts-workerpool-license-entitlement}


When you try to create a new worker pool with the `Apply my OCP entitlement` option, the creation fails and you see an error message similar the following example. 
{: tsSymptoms}

```sh
The entitlement `ocp_entitled` was not found. Specify `ocp_entitled` to search for any supported license or entitlement. 
If no match is found, then you do not have a supported license or entitlement.
```
{: screen}

The Cloud Pak license might not be assigned to your IBM Cloud account.
{: tsCauses}

Follow the steps to check your existing licenses and to assign the Cloud Pak license to your IBM Cloud account. 
{: tsResolve}

Before you begin, make sure you have at least the Editor platform access role for License and Entitlement. 

1. Log in to the [IBM Cloud console](https://cloud.ibm.com/){: external} and navigate to `Manage` > `Account`.
2. Click `Licenses and entitlements`.
3. Check if the correct Cloud Pak license is assigned to your account. 
4. If the Cloud Pak license is not assigned to your account, navigate to [IBM Passport Advantage](https://www.ibm.com/software/passportadvantage/index.html){: external} to assign the license to the account. 
