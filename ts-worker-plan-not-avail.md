---

copyright: 
  years: 2025, 2025
lastupdated: "2025-06-24"


keywords: kubernetes, openshift, user permissions, infrastructure credentials

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why do I see a `Registration failed` error when I try to provision or reload worker nodes?
{: #ts-worker-plan-not-avail}


When you try to to provision or reload worker nodes, the action fails and you see an error similar to the following.
{: tsSymptoms}

```sh
Registration failed – The plan containers.kubernetes.vpc.gen2.roks is not available in <region>. Please review the private catalog management configuration for the account.
```
{: screen}

Enterprise level catalog settings might have exclusions configured for {{site.data.keyword.openshiftlong_notm}} that block the worker node provisioning. 
{: tsCauses}

Check your Enterprise level catalog settings and remove any exclusions for {{site.data.keyword.openshiftlong_notm}}. Note that this can only be completed at the Enterprise account level and requires the Administrator level access role for the catalog management service. 
{: tsResolve}

1. In the console, navigate to the [Catalog settings](https://cloud.ibm.com/content-mgmt/catalog-settings){: external}. 
2. In the `What products are available?` section, check both steps to make sure there are no configurations that would exclude {{site.data.keyword.openshiftlong_notm}}. If there are, remove them. Make sure that there are no private catalog rules that exclude {{site.data.keyword.openshiftlong_notm}}.
3. In the `Preview` section, use the table search function to make sure that {{site.data.keyword.openshiftlong_notm}} is included in the account's private catalogs. 
4. Try again to provision or reload the worker nodes. 
