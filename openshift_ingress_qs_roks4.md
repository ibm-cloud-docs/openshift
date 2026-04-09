---

copyright:
  years: 2014, 2026
lastupdated: "2026-04-09"


keywords: openshift, nginx, ingress controller

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}


# Quick start for Ingress
{: #ingress-qs-roks4}

Quickly expose your app to the Internet by creating an Ingress resource.
{: shortdesc}

## Before you begin
{: #ingress-qs-prereqs}

- You must have an app deployed in your cluster. If you don't have an app deployed yet, see [Deploying apps in {{site.data.keyword.redhat_openshift_notm}} clusters](/docs/openshift?topic=openshift-deploy_app).
- Make sure you have the [**Writer** or **Manager** {{site.data.keyword.cloud_notm}} IAM service access role](/docs/openshift?topic=openshift-iam-platform-access-roles) for the cluster.
- [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

Not sure whether to use Ingress or Routes? See [Choosing among load balancing solutions](/docs/openshift?topic=openshift-cs_network_planning#load-balancing-comparison).
{: tip}

## Exposing your app with Ingress
{: #ingress-qs-steps}

1. Create a Kubernetes `ClusterIP` service for your app deployment.
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
