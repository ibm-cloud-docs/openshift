---

copyright:
  years: 2022, 2022
lastupdated: "2022-12-01"

keywords: openshift, ingress, troubleshoot ingress, ingress operator, ingress cluster operator, external service missing, erresnf

subcollection: openshift
content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}



# Why is the Ingress external service missing from my cluster?
{: #ts-ingress-erresnf}
{: troubleshoot}
{: support}

Supported infrastructure providers
:   Satellite

You can use the the `ibmcloud oc ingress status-report ignored-errors add` command to add an error to the ignored-errors list. Ignored errors still appear in the output of the `ibmcloud oc ingress status-report get` command, but are ignored when calculating the overall Ingress Status.
{: tip}


When you check the status of your cluster's Ingress components by running the `ibmcloud oc ingress status-report get` command, you see an error similar to the following.
{: tsSymptoms}

```sh
The external service is missing (ERRESNF).
```
{: screen}



The service that exposes the default Ingress Controller is missing from the cluster.
{: tsCauses}


Check the external service and create it if it doesn't exist.
{: tsResolve}

1. Get the details of the external service.
    ```sh
    oc get service -n openshift-ingress router-external-default
    ```
    {: pre}


1. Get the external IP addresses of your worker nodes by running the following command. Make a note of the addresses in the `EXTERNAL-IP` column.
    ```sh
    kubectl get nodes -o wide
    ```
    {: pre}
    
1. Save the following Service configuration as a YAML file called `service.yaml`.

    ```yaml
    apiVersion: v1
    kind: Service
    metadata:
      labels:
        ingresscontroller.operator.openshift.io/owning-ingresscontroller: default
      name: router-external-default
      namespace: openshift-ingress
    spec:
      ports:
      - name: http
        port: 80
        protocol: TCP
        targetPort: http
      - name: https
        port: 443
        protocol: TCP
        targetPort: https
      selector:
        ingresscontroller.operator.openshift.io/deployment-ingresscontroller: default
      externalIPs:
      - x.x.x.x # Add your worker node external IP addresses.
    ```
    {: codeblock}
    
1. Add the external IP addresses of your worker nodes that you retreived earlier in the `spec.externalIPs` list.

1. Create the service.
    ```sh
    kubectl create -f service.yaml
    ```
    {: pre}

1. Wait 10 to 15 minutes, then check if the warning is resolved. 

1. If the issue persists, contact support. Open a [support case](/docs/get-support?topic=get-support-using-avatar). In the case details, be sure to include any relevant log files, error messages, or command outputs.




