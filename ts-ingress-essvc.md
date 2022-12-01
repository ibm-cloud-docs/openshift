---

copyright: 
  years: 2022, 2022
lastupdated: "2022-12-01"

keywords: openshift, essvc

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# Why does the Ingress status show an ESSVC error?
{: #ts-ingress-essvc}
{: troubleshoot}
{: support}

Supported infrastructure providers
:   Classic
:   VPC
:   {{site.data.keyword.satelliteshort}}

When you check the status of your cluster's Ingress components by running the `ibmcloud oc ingress status-report get` command, you see an error similar to the following example.
{: tsSymptoms}

```sh
CRN does not match default secret with the same domain (ESSVC).
```
{: screen}

There are secrets in multiple namsepaces for the same domain in your cluster but they reference different {{site.data.keyword.secrets-manager_full_notm}} CRNs.
{: tsCauses}

Ensure all secrets that share the same domain have the same CRN.
{: tsResolve}

1. View all the Ingress secrets for your cluster by running the following command.

    ```sh
    ibmcloud oc ingress secret ls
    ```
    {: pre}
    
1. In the output, ensure that secrets that have the same domain also have the same CRN. For secrets that have a different CRN, update them with the correct CRN by running the following command.
    ```sh
    ibmcloud oc ingress secret update -c <cluster> --name <secret_name> --namespace <secret_namespace> --cert-crn <new_crn>
    ```
    {: pre}
    
    To find the correct CRN for the {{site.data.keyword.openshiftlong_notm}} managed domains look for the secret in the `openshift-ingress`, or `ibm-cert-store` namespaces.
    {: tip}


1. If the issue persists, contact support. Open a [support case](/docs/get-support?topic=get-support-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.


