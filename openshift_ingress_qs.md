---

copyright:
  years: 2014, 2019
lastupdated: "2019-12-19"

keywords: openshift, roks, rhoks, rhos, nginx, ingress controller

subcollection: containers

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:preview: .preview}

# Quick start for Ingress
{: #ingress-qs}

Quickly expose your app to the Internet by creating an Ingress resource.
{: shortdesc}

1. Create a Kubernetes ClusterIP service for you app so that it can be included in the Ingress application load balancing.
  ```
  oc expose deploy <app_deployment_name> --name my-app-svc --port <app_port> -n <namespace>
  ```
  {: pre}

2. Get the Ingress subdomain and secret for your cluster.
    ```
    ibmcloud oc cluster get -c <cluster_name_or_ID> | grep Ingress
    ```
    {: pre}
    Example output:
    ```
    Ingress Subdomain:      mycluster-a1b2cdef345678g9hi012j3kl4567890-0000.us-south.containers.appdomain.cloud
    Ingress Secret:         mycluster-a1b2cdef345678g9hi012j3kl4567890-0000
    ```
    {: screen}

3. Using the Ingress subdomain and secret, create an Ingress resource file. Replace `<app_path>` with the path that your app listens on. If you app does not listen on a specific path, define the root path as a slash (<code>/</code>) only.
  ```
  apiVersion: extensions/v1beta1
  kind: Ingress
  metadata:
    name: myingressresource
  spec:
    tls:
    - hosts:
      - <ingress_subdomain>
      secretName: <ingress_secret>
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

4. Create the Ingress resource.
  ```
  oc apply -f myingressresource.yaml
  ```
  {: pre}

5. In a web browser, enter the Ingress subdomain and the path for your app.
  ```
  https://<ingress_subdomain>/<app_path>
  ```
  {: codeblock}

