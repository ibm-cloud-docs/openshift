---

copyright: 
  years: 2022, 2024
lastupdated: "2024-10-30"


keywords: openshift, essec

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}



# Why does the Ingress status show an ESSEC error?
{: #ts-ingress-essec}
{: troubleshoot}
{: support}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [{{site.data.keyword.satelliteshort}}]{: tag-satellite}

When you check the status of your cluster's Ingress components by running the `ibmcloud oc ingress status-report get` command, you see an error similar to the following example.
{: tsSymptoms}

```sh
The certificate for TLS secret expired or will expire soon (ESSEC).
```
{: screen}

You have secrets in your cluster that have either expired or are about to expire in the next 5 days.
{: tsCauses}

Review and update your secrets and domains.
{: tsResolve}

1. Run the **`ibmcloud oc ingress secret ls`** command and review the output.

    For secrets that are about to expire and are user managed
    :   Ensure the value of the corresponding secret in {{site.data.keyword.secrets-manager_full_notm}} has been updated and run the **`ibmcloud oc ingress secret update`** command for that secret.
    
    For secrets that are managed by IBM
    :   Ensure the corresponding domain is still active.
    
    To determine whether a secret is IBM managed or user managed, run the **`ibmcloud oc ingress secret get`** command and look for the `User Managed` section.
    {: tip}
    

1. View the domains for your cluster.
    ```sh
    ibmcloud oc nlb-dns ls
    ```
    {: pre}
    
    
    Example output
    ```sh
    OK
    Subdomain                                                                           Target(s)                              SSL Cert Status   SSL Cert Secret Name                            Secret Namespace    Status
    example-124567891235678912345789asfghijk-0000.us-south.containers.appdomain.cloud   example0-us-south.lb.appdomain.cloud   created           example-124567891235678912345789asfghijk-0000   openshift-ingress   OK
    ```
    {: screen}

1. Inactive domains are any in the list that do not have an associated IP address or hostname. For those domains, remove the associated secrets from your cluster by running the following command.

    ```sh
    ibmcloud oc nlb-dns secret rm
    ```
    {: pre}

1. If the issue persists, contact support. Open a [support case](/docs/account?topic=account-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.
