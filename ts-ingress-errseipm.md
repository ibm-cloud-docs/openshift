---

copyright:
  years: 2022, 2023
lastupdated: "2023-01-06"

keywords: openshift, ingress, troubleshoot ingress, ingress operator, ingress cluster operator, missing ip addresses, errseipm

subcollection: openshift
content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# Why does the Ingress status show an ERRSEIPM error?
{: #ts-ingress-errseipm}
{: troubleshoot}
{: support}

[{{site.data.keyword.satelliteshort}}]{: tag-satellite}

You can use the the `ibmcloud oc ingress status-report ignored-errors add` command to add an error to the ignored-errors list. Ignored errors still appear in the output of the `ibmcloud oc ingress status-report get` command, but are ignored when calculating the overall Ingress Status.
{: tip}

When you check the status of your cluster's Ingress components by running the `ibmcloud oc ingress status-report get` command, you see an error similar to the following example.
{: tsSymptoms}

```sh
The service is missing one or more worker IPs (ERRSEIPM).
```
{: screen}

The service that exposes the default Ingress Controller does not have all the necessary worker IP addresses.
{: tsCauses}

Add the worker IP addresses to the external Ingress service.
{: tsResolve}

1. Run the following command and make note of your worker IP addresses in the `EXTERNAL-IP` column.
    ```sh
    oc get nodes -o wide 
    ```
    {: pre}

1. Run the following command to edit the service. 
    ```sh
    oc edit service -n openshift-ingress router-external-default
    ```
    {: pre}

1. Add the IP addresses that you retreived in step 1 to the `spec.externalIPs` list.

1. Wait 10 to 15 minutes, then check if the warning is resolved by running the `ibmcloud oc ingress status-report get` command.

1. If the issue persists, contact support. Open a [support case](/docs/get-support?topic=get-support-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.


