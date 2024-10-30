---

copyright: 
  years: 2022, 2024
lastupdated: "2024-10-30"


keywords: openshift, esssmi

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}



# Why does the Ingress status show an ESSSMI error?
{: #ts-ingress-esssmi}
{: troubleshoot}
{: support}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [{{site.data.keyword.satelliteshort}}]{: tag-satellite}

When you check the status of your cluster's Ingress components by running the `ibmcloud oc ingress status-report get` command, you see an error similar to the following example.
{: tsSymptoms}

```sh
Could not access Secrets Manager instance (ESSSMI).
```
{: screen}

{{site.data.keyword.openshiftlong_notm}} receives an unauthorized message when attempting to update or apply secrets from the {{site.data.keyword.secrets-manager_short}} instance registered with the cluster.
{: tsCauses}

1. Follow the steps to ensure you have a valid [service-to-service authorization policy](/docs/openshift?topic=openshift-secrets-mgr#secrets-mgr_setup_s2s) in place for the Kubernetes Service and {{site.data.keyword.secrets-manager_short}}.
{: tsResolve}

1. If the issue persists, contact support. Open a [support case](/docs/account?topic=account-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.
