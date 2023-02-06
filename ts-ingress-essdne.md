---

copyright: 
  years: 2022, 2023
lastupdated: "2023-02-06"

keywords: openshift, essdne

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}



# Why does the Ingress status show an ESSDNE error?
{: #ts-ingress-essdne}
{: troubleshoot}
{: support}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [{{site.data.keyword.satelliteshort}}]{: tag-satellite}

When you check the status of your cluster's Ingress components by running the **`ibmcloud oc ingress status-report get`** command, you see an error similar to the following example.
{: tsSymptoms}

```sh
The secret is not present on the cluster or is in the wrong namespace (ESSDNE).
```
{: screen}

A secret created via the **`ibmcloud oc ingress secret create`** command was manually deleted from the cluster.
{: tsCauses}

If the secret is no longer needed, delete it. If the secret is still needed, reapply it to the cluster.
{: tsResolve}


- If the secret is no longer needed, run the **`ibmcloud oc ingress secret rm`** command to remove it from the managed secret list.
- If the secret is still needed, run the **`ibmcloud oc ingress secret update`** command to reapply the secret to the cluster.


If the issue persists, contact support. Open a [support case](/docs/get-support?topic=get-support-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.



