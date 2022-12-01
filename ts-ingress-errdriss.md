---

copyright: 
  years: 2022, 2022
lastupdated: "2022-12-01"

keywords: openshift, errdriss, secret generation failed

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# Why does the Ingress status show an ERRDRISS error?
{: #ts-ingress-errdriss}
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
The subdomain has DNS resolution issues (ERRDRISS).
```
{: screen}


One or more managed subdomains that belong to your cluster are not resolving correctly. Your subdomain configuration might be incorrect or the backend IPs have health issues.
{: tsCauses}

Review and update your managed subdomains.
{: tsResolve}

1. Get the list of the managed domains using the **`ibmcloud oc nlb-dns ls`** [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_nlb-dns-ls).

1. Use `dig` to resolve your domains and verify that they resolve to the configured addresses.
    ```sh
    dig <subdomain>
    ```
    {: pre}
    
1. If you get `NXDOMAIN` or you see missing addresses, verify that your domain has correct configuration.

    - Make sure that the domain does not have mixed IP address types. For example, make sure the domain contains only public or only private IP addresses.
    - Make sure that the domain does not have malformed IP addresses or load balancer hostnames registered.
    
1. Check if the domain has health monitoring.
    - Get the list of the subdomain that have health monitoring enabled using the **`ibmcloud oc nlb-dns monitor ls`** [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_nlb-dns-monitor-ls).
    - If the domain is included in the list, verify whether the backend applications are healthy.
    - To see the health checking parameters, you can use the **`ibmcloud oc nlb-dns monitor get`** [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_nlb-dns-monitor-get) command.
    - Fix any backend or NLB-DNS health monitor configuration issues.
    
1. Wait 10-15 minutes, then check if the warning is resolved.


1. If the issue persists, contact support. Open a [support case](/docs/get-support?topic=get-support-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.


