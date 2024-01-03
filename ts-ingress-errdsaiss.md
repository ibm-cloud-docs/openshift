---

copyright: 
  years: 2023, 2024
lastupdated: "2024-01-03"


keywords: openshift, errdsaiss, ingress, domain, third party, external domain

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}

# Why does the Ingress status show an `ERRDSAISS` error?
{: #ts-ingress-errdsaiss}
{: troubleshoot}
{: support}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [{{site.data.keyword.satelliteshort}}]{: tag-satellite}


You can use the `ibmcloud oc ingress status-report ignored-errors add` command to add an error to the ignored-errors list. Ignored errors still appear in the output of the `ibmcloud oc ingress status-report get` command, but are ignored when calculating the overall Ingress status.
{: tip}

When you check the status of your cluster's Ingress components by running the `ibmcloud oc ingress status-report get` command, you see an error similar to the following example.
{: tsSymptoms}


```sh
The external provider for the given subdomain has authorization issues (ERRDSAISS).
```
{: screen}


The Kubernetes Service is unable to access the external domain provider used for the given subdomain.
{: tsCauses}

Complete the following steps based on your external domain provider.
{: tsResolve}


- For external Akamai or Cloudflare domains, make sure that you create a valid credential for the cluster by using **`ibmcloud ks ingress domain credential set`** command.

- For domains provisioned with Cloud Internet Services, ensure that the service-to-service authorization is in place. For more information, see [Setting up domains with IBM Cloud Internet Services](/docs/openshift?topic=openshift-ingress-domains&interface=cli#ingress-domain-cis). If you no longer want to use the domain you registered, then you can remove it by using the **`ibmcloud ks ingress domain rm --c CLUSTER --domain DOMAIN`** command.



