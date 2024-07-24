---

copyright: 
  years: 2014, 2024
lastupdated: "2024-07-24"


keywords: openshift, kubernetes, help, network, connectivity, ingress, must gather

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# Gathering Ingress logs
{: #ingress-must-gather}
{: support}

Run the following commands to gather the required logs for debugging Ingress.
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
    



1. List Ingresses.
    ```sh
    oc get ingress -n openshift-ingress
    ```
    {: pre}

1. Get the logs of the Ingress controller.
    ```sh
    oc logs ingresscontroller -n openshift-ingress-operator
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
    
Review the output for error messages, then review the list of [Ingress and routers troubleshooting topics](/docs/openshift?topic=openshift-ingress-status) for help resolving common Ingress issues.
{: tip}



