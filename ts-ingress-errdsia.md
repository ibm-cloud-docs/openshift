---

copyright: 
  years: 2022, 2024
lastupdated: "2024-01-18"


keywords: openshift, errdsia, nlb-dns, dns add, dns remove

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}



# Why does the Ingress status show an `ERRDSIA` error?
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

1. Get the list of the managed domains using the **`ibmcloud oc ingress domain ls`** [command](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-domain-ls).

1. Get the list of LoadBalancer services from your cluster.
    ```sh
    oc get services -A | grep LoadBalancer
    ```
    {: pre}
    
1. Compare the outputs of the two previous commands and identify the subdomains that have incorrect addresses registered.

1. If you no longer need a specific domain, you can use the **`ibmcloud oc ingress domain rm`** [command](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-domain-rm) to remove it.

1. If you still need the domain, you can update the registered addresses for the domain by using the **`ibmcloud oc ingress domain update`** [command](/docs/openshift?topic=openshift-kubernetes-service-cli#ingress-domain-update) command.
    
    Note that you must include all addresses you want to be registered as the update operation replaces the currently registered addresses. For example, if `52.137.182.166` is currently registered to your domain and you want to add `52.137.182.270`, you must specify `--ip 52.137.182.166 --ip 52.137.182.270` in the command.
    {: important}
    
1. Wait a 15-30 minutes, then check if the warning is resolved.

1. If the issue persists, contact support. Open a [support case](/docs/get-support?topic=get-support-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.


