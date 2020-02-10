---

copyright:
  years: 2014, 2020
lastupdated: "2020-02-10"

keywords: openshift, roks, rhoks, rhos, nginx, ingress controller

subcollection: openshift

---

{:codeblock: .codeblock}
{:deprecated: .deprecated}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:gif: data-image-type='gif'}
{:help: data-hd-content-type='help'}
{:important: .important}
{:new_window: target="_blank"}
{:note: .note}
{:pre: .pre}
{:preview: .preview}
{:screen: .screen}
{:shortdesc: .shortdesc}
{:support: data-reuse='support'}
{:table: .aria-labeledby="caption"}
{:tip: .tip}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}


# Quick start for Ingress in OpenShift version 4.3 and later
{: #ingress-qs-roks4}

Quickly expose your app to the Internet by creating an Ingress resource.
{: shortdesc}

First time setting up Ingress? Check out [Setting up Ingress in OpenShift version 4.3 or later](/docs/openshift?topic=openshift-ingress-roks4) for prerequisite steps and more details. Come back to these quick start steps for a brief refresher the next time you set up an Ingress resource.
{: tip}

<img src="images/icon-version-43.png" alt="Version 4.3 icon" width="30" style="width:30px; border-style: none"/> This quick start is for clusters that run OpenShift version 4.3 or later only. For clusters that run OpenShift version 3.11, see [Quick start for Ingress in OpenShift version 3.11](/docs/openshift?topic=openshift-ingress-qs).
{: note}

1. Create a Kubernetes `ClusterIP` service for you app so that it can be included in the router load balancing.
  ```
  oc expose deploy <app_deployment_name> --name my-app-svc --port <app_port> -n <project>
  ```
  {: pre}

2. Get the Ingress subdomain for your cluster.
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

3. Using the Ingress subdomain, create an Ingress resource file. Replace `<app_path>` with the path that your app listens on. If you app does not listen on a specific path, define the root path as a slash (<code>/</code>) only.
  ```yaml
  apiVersion: extensions/v1beta1
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
  ```
  oc apply -f myingressresource.yaml -n <project>
  ```
  {: pre}

5. In a web browser, enter the Ingress subdomain and the path for your app.
  ```
  https://<ingress_subdomain>/<app_path>
  ```
  {: codeblock}


