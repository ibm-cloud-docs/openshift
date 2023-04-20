---

copyright:
  years: 2023, 2023
lastupdated: "2023-04-20"

keywords: ingress, expose apps, privately expose, private ingress, ingress vpc

subcollection: containers

---

{{site.data.keyword.attribute-definition-list}}


# Privately exposing apps with Ingress
{: #ingress-private-expose}

Privately expose multiple apps in your {{site.data.keyword.openshiftlong}} cluster by creating Ingress resources that are managed by the Ingress controller.
{: shortdesc}

## Prerequisites
{: #ingress-private-prereqs}

Before you get started with Ingress, review the following prerequisites.
{: shortdesc}

- Setting up Ingress requires the following [{{site.data.keyword.cloud_notm}} IAM roles](/docs/openshift?topic=openshift-users):
    - **Administrator** platform access role for the cluster in {{site.data.keyword.containerlong_notm}}.
    - **Manager** service access role in all {{site.data.keyword.containerlong_notm}} namespaces ({{site.data.keyword.redhat_openshift_notm}} projects).
- If a zone fails, you might see intermittent failures in requests to apps that are exposed by the Ingress controller in that zone.
- To ensure high availability, at least two worker nodes per zone are recommended.
* VPC clusters: [Allow traffic requests that are routed by Ingress to node ports on your worker nodes](/docs/openshift?topic=openshift-vpc-security-group).
* VPC multizone clusters: If you created a cluster in the CLI and later manually added zones to your worker pools with the `ibmcloud oc zone add vpc-gen2` command, you must [update the VPC load balancer that exposes the Ingress controller](/docs/openshift?topic=openshift-router-mzr-error) to include subnets for all zones in your cluster.
* Classic clusters: Enable a [Virtual Router Function (VRF)](/docs/account?topic=account-vrf-service-endpoint#vrf) for your IBM Cloud infrastructure account.  To check whether a VRF is already enabled, use the `ibmcloud account show` command. If you can't or don't want to enable VRF, enable [VLAN spanning](/docs/vlans?topic=vlans-vlan-spanning#vlan-spanning). When a VRF or VLAN spanning is enabled, the Ingress controller can route packets to various subnets in the account.

## Privately exposing apps with a public cloud service endpoint
{: #ingress-private-se}

[Classic clusters]{: tag-classic-inf} [Virtual Private Cloud]{: tag-vpc} 

If your cluster is created on classic infrastructure, or if your cluster is created on VPC infrastructure and you enabled the public cloud service endpoint during cluster creation, your cluster is created with only a public Ingress controller by default. To privately expose your apps, you must first create a private Ingress controller. Then, you must register your Ingress controller with a subdomain and, optionally, import your own TLS certificate.
{: shortdesc}


### Step 1: Deploy apps and create app services
{: #ingress-private-se-1}

Start by deploying your apps and creating Kubernetes services to expose them.
{: shortdesc}

1. [Deploy your app to the cluster](/docs/openshift?topic=openshift-openshift_apps). Ensure that you add a label to your deployment in the metadata section of your configuration file, such as `app: code`. This label is needed to identify all pods where your app runs so that the pods are in the Ingress load balancing.

2. For each app deployment that you want to expose, create a Kubernetes `ClusterIP` service. Your app must be exposed by a Kubernetes service to be included in the Ingress load balancing.

```sh
oc expose deploy <app_deployment_name> --name my-app-svc --port <app_port> -n <namespace>
```
{: pre}
    

### Step 2: Set up TLS termination with TLS certificates and Kubernetes secrets
{: #ingress-private-tls}

Your TLS certificate must be stored as a Kubernetes secret in each namespace where your apps exist.
{: shortdesc}

#### TLS secrets for custom domains
{: #ingress-private-tls-custom}

To set up TLS secrets for a domain that you created yourself, such as a domain registered with an external provider, see [Setting up TLS secrets for custom subdomains](/docs/openshift?topic=openshift-secrets#tls-custom). These steps apply for both classic and VPC clusters. 

#### TLS secrets for the IBM-managed domain
{: #ibm-domain-tls-vpc}

* [Classic clusters]{: tag-classic-inf} To use the IBM-managed Ingress domain in a classic cluster, see [Setting up TLS secrets for the IBM-provided Ingress subdomain](/docs/containers?topic=containers-secrets#tls-default).

* [VPC clusters]{: tag-vpc} To use the IBM-managed Ingress domain in a VPC cluster, follow these steps.

1. List the existing subdomains in your cluster. In the **Subdomain** column of the output, copy the subdomain that has the highest `000<n>` value.
    ```sh
    ibmcloud oc nlb-dns ls --cluster <cluster_name_or_id>
    ```
    {: pre}

    In this example output, the `mycluster-a1b2cdef345678g9hi012j3kl4567890-0002.us-south.containers.appdomain.cloud` subdomain has the highest `000<n>` value of `0002`.
    ```sh
    Subdomain                                                                               Load Balancer Hostname                        Health Monitor   SSL Cert Status           SSL Cert Secret Name
    mycluster-a1b2cdef345678g9hi012j3kl4567890-0000.us-south.containers.appdomain.cloud     ["1234abcd-us-south.lb.appdomain.cloud"]      None             created                   mycluster-a1b2cdef345678g9hi012j3kl4567890-0000
    mycluster-a1b2cdef345678g9hi012j3kl4567890-0001.us-south.containers.appdomain.cloud     ["5678efgh-us-south.lb.appdomain.cloud"]      None             created                   mycluster-a1b2cdef345678g9hi012j3kl4567890-0001
    mycluster-a1b2cdef345678g9hi012j3kl4567890-0002.us-south.containers.appdomain.cloud     ["9012ijkl-us-south.lb.appdomain.cloud"]      None             created                   mycluster-a1b2cdef345678g9hi012j3kl4567890-0002
    ```
    {: screen}

2. In the subdomain that you copied, change the `000<n>` value in the subdomain to `i00<n+1>`. For example, the `mycluster-a1b2cdef345678g9hi012j3kl4567890-0002.us-south.containers.appdomain.cloud` subdomain is changed to `mycluster-a1b2cdef345678g9hi012j3kl4567890-i003.us-south.containers.appdomain.cloud`. The `i` value indicates a private subdomain, and the `n+1` value indicates the next consecutive subdomain that you create in this cluster. You register this subdomain in later steps. When you register the domain, a TLS secret for the domain is automatically generated. The secret name follows a truncated format of the subdomain, such as `mycluster-a1b2cdef345678g9hi012j3kl4567890-i003`.

### Step 3: Create and configure a private Ingress controller
{: #ingress-private-se-3}

After you get your domain and TLS certificate ready, you must create a private Ingress controller and configure the controller with your domain.
{: shortdesc}

1. Create a configuration file for a private Ingress controller.
    ```yaml
    apiVersion: operator.openshift.io/v1
    kind: IngressController
    metadata:
      name: private-ingress-controller
      namespace: openshift-ingress-operator
    spec:
      replicas: 2
      domain: <domain>
      endpointPublishingStrategy:
        loadBalancer:
          scope: Internal
        type: LoadBalancerService
    ```
    {: codeblock}

2. Create the IngressController resource in the `openshift-ingress-operator` project of your cluster. When you create the IngressController, a private Ingress controller is automatically created and deployed in the `openshift-ingress` project based on the IngressController settings that you set in the previous step. Additionally, an Ingress controller service is created to expose the Ingress controller with an IP address (classic clusters) or a VPC hostname (VPC clusters).
    ```sh
    oc create -f private-ingress-controller.yaml -n openshift-ingress-operator
    ```
    {: pre}

3. Run the **`oc get`** command and find the IP address or VPC hostname in the **EXTERNAL IP** field of the `router-private-ingress-controller` service.
    ```sh
    oc get svc router-private-ingress-controller -n openshift-ingress
    ```
    {: pre}

    Example output for classic clusters.
    ```sh
    NAME                                  TYPE           CLUSTER-IP       EXTERNAL-IP    PORT(S)                      AGE
    router-private-ingress-controller     LoadBalancer   172.21.57.132    10.XX.XX.XX    80/TCP,443/TCP,1940/TCP      3m
    ```
    {: screen}

    Example output for VPC clusters:
    ```sh
    NAME                                  TYPE           CLUSTER-IP       EXTERNAL-IP                             PORT(S)                      AGE
    router-private-ingress-controller     LoadBalancer   172.21.57.132    1234abcd-us-south.lb.appdomain.cloud    80/TCP,443/TCP,1940/TCP      3m
    ```
    {: screen}

4. Register the service's external IP address or VPC hostname with the domain you previously chose.
    * Custom domain: Work with your DNS provider to add the `router-private-ingress-controller` service's external IP address as an A record (classic clusters) or VPC hostname as a CNAME (VPC clusters) that maps to your custom domain.
    * IBM-provided domain: Create a DNS entry for the `router-private-ingress-controller` service's VPC hostname. When you run the following command, the subdomain that you specified in the `private-ingress-controller.yaml` file is automatically generated, and is registered with the `router-private-ingress-controller` service. A TLS secret for the domain is automatically generated in the project that you specify where your app runs. The secret name follows a truncated format of the subdomain, such as `mycluster-a1b2cdef345678g9hi012j3kl4567890-i003`.
        ```sh
        ibmcloud oc nlb-dns create vpc-gen2 --cluster <cluster_name_or_ID> --lb-host <VPC_hostname> --type private --secret-namespace <project>
        ```
        {: pre}



### Step 4: Create the Ingress resource
{: #ingress-private-se-4}

Ingress resources define the routing rules that the Ingress controller uses to route traffic to your app service.
{: shortdesc}

1. Define an Ingress resource configuration file that uses the IBM-provided domain or your custom domain to route incoming network traffic to the services that you created earlier.
    ```yaml
    apiVersion: networking.k8s.io/v1 # For 4.5 or earlier, use networking.k8s.io/v1beta1 instead
    kind: Ingress
    metadata:
      name: myingressresource
    spec:
      tls:
      - hosts:
        - <subdomain>
        secretName: <custom_secret_name>
      rules:
      - host: <subdomain>
        http:
          paths:
          - path: /<app1_path>
            backend:
                service:
                    name: <app1_service>
                    port:
                        number: 80
          - path: /<app2_path>
            backend:
                serivce:
                  name: <app2_service>
                  port:
                    number: 80
    ```
    {: codeblock}

    `tls`
    :    If you want to use TLS, include this TLS section in your resource. Replace `<domain>` with your subdomain. Do not use `*` for your host or leave the host property empty to avoid failures during Ingress creation.
    :    Replace `<tls_secret_name>` with the secret that you created earlier that holds your TLS certificate and key for a custom domain or the TLS secret that was automatically generated for an IBM-provided subdomain.

    `host`
    :    Replace `<domain>` with your subdomain.
    :    If your cluster has multiple projects where apps are exposed, one Ingress resource is required per project. You can use the same subdomain in each resource or different subdomains in each resource. For example, if you use a wildcard domain, you can append a wildcard subdomain to the beginning of the domain, such as `subdomain1.custom_domain.net`.
    :    Do not use `*` for your host or leave the host property empty to avoid failures during Ingress creation.

    `path`
    :   Replace `<app_path>` with the path that your app is listening on. The path is appended to the IBM-provided or your custom domain to create a unique route to your app. When you enter this route into a web browser, network traffic is routed to the Ingress controller. The Ingress controller looks up the associated service, and sends network traffic to the service. The service then forwards the traffic to the pods where the app runs. Many apps don't listen on a specific path, but use the root path and a specific port. In this case, define the root path as `/` and don't specify an individual path for your app.
    :    For example, to use `http://domain/`, enter `/` as the path. For `http://domain/app1_path`, enter `/app1_path` as the path.

    `serviceName`
    :    Replace `<app1_service>` and `<app2_service>`, and so on, with the name of the services you created to expose your apps. If your apps are exposed by services in different projects in the cluster, include only app services that are in the same project. You must create one Ingress resource for each project that contains apps that you want to expose.

    `servicePort`
    :    The port that your service listens to. Use the same port that you defined when you created the Kubernetes service for your app.



2. Create the Ingress resource for your cluster. Ensure that the resource deploys into the same project as the app services that you specified in the resource.
    ```sh
    oc apply -f myingressresource.yaml -n <project>
    ```
    {: pre}

3. Verify that the Ingress resource was created successfully. If messages in the events describe an error in your resource configuration, fix the values in your resource file and reapply the file for the resource.
    ```sh
    oc describe ingress myingressresource
    ```
    {: pre}

Your Ingress resource is created in the same project as your app services, and your apps are registered with the Ingress controller.



### Step 5: Access your app from your private network
{: #ingress-private-se-5}

1. Classic clusters: Before you can access your app, make sure that you can access a DNS service. To use the default external DNS provider, you must [configure edge nodes with public access](/docs/openshift?topic=openshift-edge#edge) and [configure a Virtual Router Appliance](https://www.ibm.com/blogs/cloud-archive/2017/07/kubernetes-and-bluemix-container-based-workloads-part4/){: external}.

2. From within your private network, enter the URL of the app service in a web browser.

    ```sh
    https://<domain>/<app1_path>
    ```
    {: codeblock}

    If you exposed multiple apps, access those apps by changing the path that is appended to the URL.

    ```sh
    https://<domain>/<app2_path>
    ```
    {: codeblock}

    If you use a wildcard domain, access those apps with their own subdomains.

    ```sh
    http://<subdomain1>.<domain>/<app1_path>
    ```
    {: codeblock}

    ```sh
    http://<subdomain2>.<domain>/<app1_path>
    ```
    {: codeblock}

Can't connect to your app through Ingress? Try [Troubleshooting Ingress](/docs/openshift?topic=openshift-ingress-status).
{: tip}

## Privately exposing apps in VPC clusters with a private cloud service endpoint only
{: #priv-se-priv-controller}

If your cluster is created on VPC infrastructure and you enabled only the private cloud service endpoint when you created the cluster, you can use the default private Ingress controller to expose apps in your cluster to requests from the private network.
{: shortdesc}

### Step 1: Deploy apps and create app services
{: #priv-se-priv-controller-1}

Start by deploying your apps and creating Kubernetes services to expose them.
{: shortdesc}

1. [Deploy your app to the cluster](/docs/openshift?topic=openshift-openshift_apps). Ensure that you add a label to your deployment in the metadata section of your configuration file, such as `app: code`. This label is needed to identify all pods where your app runs so that the pods are in the Ingress load balancing.

2. For each app deployment that you want to expose, create a Kubernetes `ClusterIP` service. Your app must be exposed by a Kubernetes service to be included in the Ingress load balancing.

```sh
oc expose deploy <app_deployment_name> --name my-app-svc --port <app_port> -n <namespace>
```
{: pre}
    


### Step 2: Set up TLS termination with TLS certificates and Kubernetes secrets
{: #managed-ingress-steps-tls-private}

Your TLS certificate must be stored as a Kubernetes secret in each namespace where your apps exist.
{: shortdesc}

* To use the IBM-managed Ingress domain, see [Setting up TLS secrets for the IBM-provided Ingress subdomain](/docs/containers?topic=containers-secrets#tls-default).

* To use a domain that you created yourself, such as a domain registered with an external provider, see [Setting up TLS secrets for custom subdomains](/docs/containers?topic=containers-secrets#tls-custom).

### Step 3: Create the Ingress resource
{: #priv-se-priv-controller-3}

Ingress resources define the routing rules that the Ingress controller uses to route traffic to your app service.
{: shortdesc}

1. Define an Ingress resource configuration file that uses the IBM-provided domain or your custom domain to route incoming network traffic to the services that you created earlier.
    ```yaml
    apiVersion: networking.k8s.io/v1 # For 4.5 or earlier, use networking.k8s.io/v1beta1 instead
    kind: Ingress
    metadata:
      name: myingressresource
    spec:
      tls:
      - hosts:
        - <custom_domain>
        secretName: <custom_secret_name>
      rules:
      - host: <domain>
        http:
          paths:
          - path: /<app1_path>
            backend:
                service:
                  name: <app1_service>
                  port:
                    number: 80
          - path: /<app2_path>
            backend:
                service:
                  name: <app2_service>
                  port:
                    number: 80
    ```
    {: codeblock}


    `tls`
    :    If you want to use TLS, include this TLS section in your resource.
    :    Replace `<domain>` with your subdomain. Do not use &ast; for your host or leave the host property empty to avoid failures during Ingress creation.
    :    Replace `<tls_secret_name>` with the secret that you created earlier that holds your TLS certificate and key for a custom domain or the TLS secret that was automatically generated for an IBM-provided subdomain.

    `host`
    :    Replace `<domain>` with the IBM-provided Ingress subdomain or your custom domain.
    :    If your cluster has multiple projects where apps are exposed, one Ingress resource is required per project. You can use the same subdomain in each resource or different subdomains in each resource. For example, if you use a wildcard domain, you can append a wildcard subdomain to the beginning of the domain, such as `subdomain1.custom_domain.net` or `subdomain1.mycluster-<hash>-0000.us-south.containers.appdomain.cloud`. Do not use`*` for your host or leave the host property empty to avoid failures during Ingress creation.

    `path`
    :   Replace `<app_path>` with the path that your app is listening on. The path is appended to the IBM-provided or your custom domain to create a unique route to your app. When you enter this route into a web browser, network traffic is routed to the Ingress controller. The Ingress controller looks up the associated service, and sends network traffic to the service. The service then forwards the traffic to the pods where the app runs. Many apps don't listen on a specific path, but use the root path and a specific port. In this case, define the root path as `/` and don't specify an individual path for your app.
    :    For example, to use `http://domain/`, enter `/` as the path. For `http://domain/app1_path`, enter `/app1_path` as the path.

    `name`
    :    Replace `<app1_service>` and `<app2_service>`, and so on, with the name of the services you created to expose your apps. If your apps are exposed by services in different projects in the cluster, include only app services that are in the same project. You must create one Ingress resource for each project where you have apps that you want to expose.

    `port`
    :    The port that your service listens to. Use the same port that you defined when you created the Kubernetes service for your app.



2. Create the Ingress resource for your cluster. Ensure that the resource deploys into the same project as the app services that you specified in the resource.
    ```sh
    oc apply -f myingressresource.yaml -n <project>
    ```
    {: pre}

3. Verify that the Ingress resource was created successfully. If messages in the events describe an error in your resource configuration, fix the values in your resource file and reapply the file for the resource.
    ```sh
    oc describe ingress myingressresource
    ```
    {: pre}

Your Ingress resource is created in the same project as your app services, and your apps are registered with the Ingress controller.



### Step 4: Access your app
{: #priv-se-priv-controller-4}

In a web browser, enter the URL of the app service to access.
{: shortdesc}

```sh
https://<domain>/<app1_path>
```
{: codeblock}

If you exposed multiple apps, access those apps by changing the path that is appended to the URL.

```sh
https://<domain>/<app2_path>
```
{: codeblock}

If you use a wildcard domain, access those apps with their own subdomains.

```sh
http://<subdomain1>.<domain>/<app1_path>
```
{: codeblock}

```sh
http://<subdomain2>.<domain>/<app1_path>
```
{: codeblock}

Can't connect to your app through Ingress? Try [Troubleshooting Ingress](/docs/openshift?topic=openshift-ingress-status).
{: tip}



