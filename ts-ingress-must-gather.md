---

copyright: 
  years: 2014, 2022
lastupdated: "2022-02-18"

keywords: openshift

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# Gathering Ingress logs
{: #ingress-must-gather}
{: support}

Run the following commands to gather the required logs for debugging Ingress.
{: shortdesc}

1. List ALBs.

    ```sh
    ibmcloud oc ingress alb ls -c CLUSTERID
    ```
    {: pre}

1. Get the Ingress status.

    ```sh
    ibmcloud oc ingress status -c CLUSTERID
    ```
    {: pre}
    
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

1. Describe your Ingress resource.

    ```sh
    oc describe ing <ingress name> -n <namespace>
    ```
    {: pre}
    
1. Get the logs for the `nginx-ingress` container in your Ingress pods.

    ```sh
    oc logs <ingress pods> -n kube-system -c nginx-ingress
    ```
    {: pre}
    
1.  List host names for network load balancer (NLB).

    ```sh
    ibmcloud oc nlb-dns ls -c CLUSTERID
    ```
    {: pre}

1. List the `alb` pods in the `kube-system` namespace.

    ```sh
    oc get pods -n kube-system | grep alb
    ```
    {: pre}
    
1. Run an `nslookup` on your Ingress subdomain.

    ```sh
    nslookup ingresssubdomain.com
    ```
    {: pre}
    
Review the output for error messages, then review the list of [Ingress and routers troubleshooting topics](/docs/openshift?topic=openshift-sitemap#sitemap_ingress_and_routers) for help resolving common Ingress issues.
{: tip}



