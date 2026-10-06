---

copyright: 
  years: 2024, 2026
lastupdated: "2026-10-06"

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

The Cloud Pak license might not be assigned to your IBM Cloud account. If your OpenShift license was acquired through Passport Advantage, the entitlement key owner's IBMid might not be added to your IBM Cloud account.
{: tsCauses}

Follow the steps to check your existing licenses and to assign the Cloud Pak license to your IBM Cloud account.
{: tsResolve}

Before you begin, complete the following prerequisite steps.

- Make sure that you have at least the Editor platform access role for the License and Entitlement account management service.
- If your OpenShift license was acquired through Passport Advantage, make sure that the entitlement key owner's IBMid is added to the IBM Cloud account where the cluster is being created, and that the owner is assigned the Administrator role on the License and Entitlement account management service.

1. Log in to the [IBM Cloud console](https://cloud.ibm.com/){: external} and navigate to `Manage` > `Account`.
2. Click `Licenses and entitlements`.
3. Check if the correct Cloud Pak license is assigned to your account. 
4. If the Cloud Pak license is not assigned to your account, navigate to [IBM Passport Advantage](https://www.ibm.com/software/passportadvantage){: external} to assign the license to the account.
