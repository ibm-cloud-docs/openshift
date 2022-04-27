---

copyright:
  years: 2014, 2022
lastupdated: "2022-04-27"

keywords: openshift, nginx, ingress controller

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}


# Quick start for Ingress
{: #ingress-qs-roks4}

Quickly expose your app to the Internet by creating an Ingress resource.
{: shortdesc}

![Version 4 icon.](images/icon-version-43.png) This quick start is for clusters that run {{site.data.keyword.redhat_openshift_notm}} version 4 only.
{: note}

1. Create a Kubernetes `ClusterIP` service for your app so that it are in the router load balancing.
    ```sh
    oc expose deploy <app_deployment_name> --name my-app-svc --port <app_port> -n <project>
    ```
    {: pre}

2. Get the Ingress subdomain for your cluster.
    ```sh
    ibmcloud oc cluster get -c <cluster_name_or_ID> | grep 'Ingress Subdomain'
    ```
    {: pre}

    Example output

    ```sh
    Ingress Subdomain:      mycluster-a1b2cdef345678g9hi012j3kl4567890-0000.us-south.containers.appdomain.cloud
    ```
    {: screen}

3. Using the Ingress subdomain, create an Ingress resource file. Replace `<app_path>` with the path that your app listens on. If your app does not listen on a specific path, define the root path as a slash (`/`) only.

    * For OpenShift 4.6 or later, use `networking.k8s.io/v1`.

        ```yaml
        apiVersion: networking.k8s.io/v1
        kind: Ingress
        metadata:
          name: myingressresource
        spec:
          rules:
          - host: <ingress_subdomain>
            http:
              paths:
              - path: /<app_path>
                pathType: ImplementationSpecific
                backend:
                  service:
                    name: my-app-svc
                    port:
                      number: 80
        ```
        {: codeblock}

    * For OpenShift 4.5 or earlier, use `networking.k8s.io/v1beta1`.

        ```yaml
        apiVersion: networking.k8s.io/v1beta1
        kind: Ingress
        metadata:
        name: myingressresource
        spec:
          rules:
          - host: <ingress_subdomain>
            http:
              paths:
              - path: /<app_path>
                backend:
                  serviceName: my-app-svc
                  servicePort: 80
        ```
        {: codeblock}

4. Create the Ingress resource in the same project as your app service.
    ```sh
    oc apply -f myingressresource.yaml -n <project>
    ```
    {: pre}

5. In a web browser, enter the Ingress subdomain and the path for your app.
    ```sh
    http://<ingress_subdomain>/<app_path>
    ```
    {: codeblock}






