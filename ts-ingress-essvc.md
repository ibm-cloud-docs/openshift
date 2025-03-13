---

copyright: 
  years: 2022, 2025
lastupdated: "2025-03-13"


keywords: openshift, essvc

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}



# Why does the Ingress status show an ESSVC error?
{: #ts-ingress-essvc}
{: troubleshoot}
{: support}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [{{site.data.keyword.satelliteshort}}]{: tag-satellite}

When you check the status of your cluster's Ingress components by running the `ibmcloud oc ingress status-report get` command, you see an error similar to the following example.
{: tsSymptoms}

```sh
The CRN does not match the default secret with the same domain (ESSVC).
```
{: screen}

There are secrets in multiple namespaces for the same domain in your cluster but they reference different {{site.data.keyword.secrets-manager_full_notm}} CRNs.
{: tsCauses}

Ensure all secrets that share the same domain have the same CRN.
{: tsResolve}

1. View all the Ingress secrets for your cluster by running the following command.

    ```sh
    ibmcloud oc ingress secret ls --show-crn
    ```
    {: pre}
    
1. In the output, ensure that secrets that have the same domain also have the same CRN. For secrets that have a different CRN, update them with the correct CRN by running the following command.
    ```sh
    ibmcloud oc ingress secret update -c <cluster> --name <secret_name> --namespace <secret_namespace> --cert-crn <new_crn>
    ```
    {: pre}
    
    To find the correct CRN for the {{site.data.keyword.openshiftlong_notm}} managed domains look for the secret in the `openshift-ingress`, or `ibm-cert-store` namespaces.
    {: tip}


1. If the issue persists, contact support. Open a [support case](/docs/account?topic=account-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.
