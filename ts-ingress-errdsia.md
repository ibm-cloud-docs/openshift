---

copyright: 
  years: 2022, 2023
lastupdated: "2023-01-06"

keywords: openshift, errdsia, nlb-dns, dns add, dns remove

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# Why does the Ingress status show an ERRDSIA error?
{: #ts-ingress-errdsia}
{: troubleshoot}
{: support}



[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf} [{{site.data.keyword.satelliteshort}}]{: tag-satellite}

You can use the the `ibmcloud oc ingress status-report ignored-errors add` command to add an error to the ignored-errors list. Ignored errors still appear in the output of the `ibmcloud oc ingress status-report get` command, but are ignored when calculating the overall Ingress Status.
{: tip}

When you check the status of your cluster's Ingress components by running the `ibmcloud oc ingress status-report get` command, you see an error similar to the following example.
{: tsSymptoms}

```sh
The subdomain has incorrect addresses registered (ERRDSIA).
```
{: screen}


Normally, the NLB-DNS subdomains should hold IP addresses or load balancer hostnames that are tied to one or more LoadBalancer services on your cluster, but one or more domains have unknown addresses registered.
{: tsCauses}

Identify and update any NLB-DNS subdomains that have incorrect addresses registered.
{: tsResolve}

1. Get the list of the managed domains using the **`ibmcloud oc nlb-dns ls`** [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_nlb-dns-ls).

1. Get the list of LoadBalancer services from your cluster:
    ```sh
    oc get services -A | grep LoadBalancer
    ```
    {: pre}
    
1. Compare the outputs and identify NLB-DNS subdomains that have incorrect addresses registered.

1. If you no longer need a specific NLB-DNS subdomain, you can use the **`ibmcloud oc nlb-dns rm`** [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_nlb-dns-rm) to unregister the addresses.

1. If you need the subdomain, you can update the addresses using the following commands.

    For subdomains that have IP addresses registered.
    :   Remove all invalid addresses using the **`ibmcloud oc nlb-dns rm`** [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_nlb-dns-rm), then add the correct IP addresses by using the **`ibmcloud oc nlb-dns add`** [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_nlb-dns-add).
    
    For subdomains that have load balancer hostnames.
    :   Run the **`ibmcloud oc nlb-dns replace`** [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_nlb-dns-replace) to update the subdomain with the correct load balancer hostname.
    
1. Wait a 15-30 minutes, then check if the warning is resolved.

1. If the issue persists, contact support. Open a [support case](/docs/get-support?topic=get-support-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.


