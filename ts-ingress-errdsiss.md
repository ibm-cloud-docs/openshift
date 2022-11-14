---

copyright: 
  years: 2022, 2022
lastupdated: "2022-11-14"

keywords: openshift, errdsiss, nlb dns

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# Why does the Ingress status show an ERRDSISS error?
{: #ts-ingress-errdsiss}
{: troubleshoot}
{: support}

Supported infrastructure providers
:   Classic
:   VPC
:   {{site.data.keyword.satelliteshort}}

You can use the the `ibmcloud oc ingress status-report ignored-errors add` command to add an error to the ignored-errors list. Ignored errors still appear in the output of the `ibmcloud oc ingress status-report get` command, but are ignored when calculating the overall Ingress Status.
{: tip}

When you check the status of your cluster's Ingress components by running the `ibmcloud oc ingress status-report get` command, you see an error similar to the following example.
{: tsSymptoms}

```sh
The subdomain has TLS secret issues (ERRDSISS).
```
{: screen}


{{site.data.keyword.openshiftlong_notm}} generates a TLS certificate for managed domains and creates a TLS secret on the cluster containing the certificate. Normally, the certificate status should be `created` or `deleted`, but the status indicates problems with the certificate or secret generation.
{: tsCauses}

Check the `SSL Cert Status` of your managed domains and, if needed, regenerate them. 
{: tsResolve}

1. Get the list of the managed domains using the **`ibmcloud oc nlb-dns ls`** [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_nlb-dns-ls).
1. Check the `SSL Cert Status` column.

    `creating` or `regenerating` status.
    :   Wait a few hours and check the status again. If the status does not change, ensure that the namespace appearing in the `Secret Namespace` exists.
    
    `rate_limited` status.
    :   Let's Encrypt refused to generate a new certificate for this domain. This usually happens when the cluster is deleted and recreated with the same name, or the **`ibmcloud oc nlb-dns secret regenerate`** command was invoked multiple times. The rate limit will expire after 7 days (there is no way to manually remove it). Certificate generation will be automatically attempted again after 7 days.
1. Wait 10-15 minutes, then check if the warning is resolved.
1. If the issue persists, contact support. Open a [support case](/docs/get-support?topic=get-support-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.


