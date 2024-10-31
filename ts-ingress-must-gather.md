---

copyright: 
  years: 2014, 2024
lastupdated: "2024-10-30"


keywords: openshift, kubernetes, help, network, connectivity, ingress, must gather

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# Gathering Ingress details for debugging
{: #ingress-must-gather}
{: support}

Run the following commands to gather the required logs and details for debugging Ingress.
{: shortdesc}

1. Get nodes and node labels.

    ```sh
    oc get nodes --show-labels
    ```
    {: pre}
    
1. Get endpoints.

    ```sh
    oc get endpoints -o wide
    ```
    {: pre}

1. Get the Ingress status.

    ```sh
    ibmcloud oc ingress status-report get -c CLUSTERID
    ```
    {: pre}
    



1. List your routes.
    ```sh
    oc get route -n openshift-ingress
    ```
    {: pre}

1. Get the logs of the Ingress controller.
    ```sh
    oc describe ingresscontroller -n openshift-ingress-operator
    ```
    {: pre}

1. Get the Ingress Operator logs.
    ```sh
    oc logs deployments/ingress-operator -n openshift-ingress-operator -c ingress-operator
    ```
    {: pre}

1. List pods in the `openshift-ingress` namespace.
    ```sh
    oc get pods -n openshift-ingress
    ```
    {: pre}

1. Get the router service details.
    ```sh
    oc get svc -n openshift-ingress
    ```
    {: pre}

1. Describe the router service.
    ```sh
    oc describe svc router-default -n openshift-ingress
    ```
    {: pre}



1. List your cluster subdomains.
    ```sh
    ibmcloud oc ingress domain ls -c CLUSTERID
    ```
    {: pre}
    
1. Run an `nslookup` on your Ingress subdomain.

    ```sh
    nslookup ingresssubdomain.com
    ```
    {: pre}
    

1. Save the information you've gathered and Open a [support case](/docs/account?topic=account-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.
