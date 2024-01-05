---

copyright:
  years: 2023, 2024
lastupdated: "2024-01-05"


keywords: ingress, expose apps, publicly expose, public ingress, ingress vpc

subcollection: openshift
---

{{site.data.keyword.attribute-definition-list}}


# Publicly exposing apps with Ingress
{: #ingress-public-expose}

Publicly expose multiple apps in your {{site.data.keyword.openshiftlong}} cluster by creating Ingress resources that are managed by the Ingress controller.
{: shortdesc}

## Prerequisites
{: #ingress-public-prereqs}

Before you get started with Ingress, review the following prerequisites.
{: shortdesc}

- Setting up Ingress requires the following [{{site.data.keyword.cloud_notm}} IAM roles](/docs/openshift?topic=openshift-users):
    - **Administrator** platform access role for the cluster in {{site.data.keyword.containerlong_notm}}.
    - **Manager** service access role in all {{site.data.keyword.containerlong_notm}} namespaces ({{site.data.keyword.redhat_openshift_notm}} projects).
- If a zone fails, you might see intermittent failures in requests to apps that are exposed by the Ingress controller in that zone.
- To ensure high availability, at least two worker nodes per zone are recommended.
* VPC clusters: [Allow traffic requests that are routed by Ingress to node ports on your worker nodes](/docs/openshift?topic=openshift-vpc-security-group).
* VPC multizone clusters: If you created a cluster in the CLI and later manually added zones to your worker pools with the `ibmcloud oc zone add vpc-gen2` command, you must [update the VPC load balancer that exposes the Ingress controller](/docs/openshift?topic=openshift-router-mzr-error) to include subnets for all zones in your cluster.
* Classic clusters: Enable a [Virtual Router Function (VRF)](/docs/account?topic=account-vrf-service-endpoint&interface=ui) for your IBM Cloud infrastructure account. To enable VRF, see [Enabling VRF](/docs/account?topic=account-vrf-service-endpoint&interface=ui). To check whether a VRF is already enabled, use the `ibmcloud account show` command. If you can't or don't want to enable VRF, enable [VLAN spanning](/docs/vlans?topic=vlans-vlan-spanning#vlan-spanning). When a VRF or VLAN spanning is enabled, the Ingress controller can route packets to various subnets in the account.

## Publicly exposing apps in clusters with a public cloud service endpoint
{: #ingress-public-se}

[Classic clusters]{: tag-classic-inf} [Virtual Private Cloud]{: tag-vpc} 

If your cluster is created on classic infrastructure, or if your cluster is created on VPC infrastructure and you enabled the public cloud service endpoint when you created it, you can use the default public Ingress controller to expose apps in your cluster to receive requests that are from the public network.
{: shortdesc}

Before you begin:
* Review the Ingress [prerequisites](#ingress-public-prereqs).
* [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

### Step 1: Deploy apps and create app services
{: #ingress-public-se-1}

Start by deploying your apps and creating Kubernetes services to expose them.
{: shortdesc}

1. [Deploy your app to the cluster](/docs/openshift?topic=openshift-app). Ensure that you add a label to your deployment in the metadata section of your configuration file, such as `app: code`. This label is needed to identify all pods where your app runs so that the pods are in the Ingress load balancing.

2. For each app deployment that you want to expose, create a Kubernetes `ClusterIP` service. Your app must be exposed by a Kubernetes service to be included in the Ingress load balancing.

```sh
oc expose deploy <app_deployment_name> --name my-app-svc --port <app_port> -n <namespace>
```
{: pre}
    

### Step 2: Set up TLS termination with TLS certificates and Kubernetes secrets
{: #managed-ingress-steps-tls-public}

Your TLS certificate must be stored as a Kubernetes secret in each namespace where your apps exist.
{: shortdesc}

* To use the IBM-managed Ingress domain, see [Setting up TLS secrets for the IBM-provided Ingress subdomain](/docs/containers?topic=containers-secrets#tls-default).

* To use a domain that you created yourself, such as a domain that is registered with an external provider, see [Setting up TLS secrets for custom subdomains](/docs/containers?topic=containers-secrets#tls-custom).


### Step 3: Create the Ingress resource
{: #ingress-public-se-3}

Ingress resources define the routing rules that the Ingress controller uses to route traffic to your app service.
{: shortdesc}

1. Define an Ingress resource configuration file that uses the IBM-provided domain or your custom domain to route incoming network traffic to the services that you created earlier.
    ```yaml
    apiVersion: networking.k8s.io/v1 
    kind: Ingress
    metadata:
      name: myingressresource
    spec:
      tls:
      - hosts:
        - <domain>
        secretName: <secret_name>
      rules:
      - host: <domain>
        http:
          paths:
          - path: /<app1_path>
            backend:
                service:
                    name: test
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
    :    If you want to use TLS, include this TLS section in your resource. Replace `<domain>` with your subdomain. Do not use `*` for your host or leave the host property empty to avoid failures during Ingress creation. Replace `<tls_secret_name>` with the secret that you created earlier that holds your TLS certificate and key for a custom domain or the TLS secret that was automatically generated for an IBM-provided subdomain.

    `host`
    :    Replace `<domain>` with the IBM-provided Ingress subdomain or your custom domain. If your cluster has multiple projects where apps are exposed, one Ingress resource is required per project. You can use the same subdomain in each resource or different subdomains in each resource. For example, if you use a wildcard domain, you can append a wildcard subdomain to the beginning of the domain, such as `subdomain1.custom_domain.net` or `subdomain1.mycluster-<hash>-0000.us-south.containers.appdomain.cloud`. Do not use &ast; for your host or leave the host property empty to avoid failures during Ingress creation.

    `path`
    :    Replace `<app_path>` with  the path that your app is listening on. The path is appended to the IBM-provided or your custom domain to create a unique route to your app. When you enter this route into a web browser, network traffic is routed to the Ingress controller. The Ingress controller looks up the associated service, and the Ingress controller sends network traffic to the service. The service then forwards the traffic to the pods where the app runs. Many apps don't listen on a specific path, but use the root path and a specific port. In this case, define the root path as `/` and don't specify an individual path for your app. For `http://domain/`, enter `/` as the path. For `http://domain/app1_path`, enter `/app1_path` as the path.

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

### Step 4: Access your app from the internet
{: #ingress-public-se-4}

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



## Publicly exposing apps in VPC clusters with a private cloud service endpoint only
{: #ingress-public-expose-vpc-private-se}

[Virtual Private Cloud]{: tag-vpc}

If your cluster is created on VPC infrastructure and you enabled only the private cloud service endpoint when you created it, your cluster is created with only a private Ingress controller by default. To publicly expose your apps, you must first create a public Ingress controller. Then, you must register your Ingress controller with a subdomain and, optionally, import your own TLS certificate.
{: shortdesc}

### Step 1: Deploy apps and create app services
{: #ingress-public-vpc-1}

Start by deploying your apps and creating Kubernetes services to expose them.
{: shortdesc}

1. [Deploy your app to the cluster](/docs/openshift?topic=openshift-app). Ensure that you add a label to your deployment in the metadata section of your configuration file, such as `app: code`. This label is needed to identify all pods where your app runs so that the pods are in the Ingress load balancing.

2. For each app deployment that you want to expose, create a Kubernetes `ClusterIP` service. Your app must be exposed by a Kubernetes service to be included in the Ingress load balancing.

```sh
oc expose deploy <app_deployment_name> --name my-app-svc --port <app_port> -n <namespace>
```
{: pre}
    

### Step 2: Set up TLS termination with TLS certificates and Kubernetes secrets
{: #managed-ingress-steps-tls}

Your TLS certificate must be stored as a Kubernetes secret in each namespace where your apps exist.
{: shortdesc}

#### TLS secrets for custom Ingress domains
{: #ingress-private-tls-custom-public}

To use a domain that you created yourself, such as a domain that is registered with an external provider, see [Setting up TLS secrets for custom subdomains](/docs/containers?topic=containers-secrets#tls-custom).
{: shortdesc}

#### TLS secrets for IBM-managed Ingress domains
{: #tls-domain-ibm-provided}

Follow the steps to set up TLS secrets for the IBM-managed Ingress domain. 
{: shortdesc}

1. List the existing subdomains in your cluster. In the **Subdomain** column of the output, copy the subdomain that has the highest `i00<n>` value.
    ```sh
    ibmcloud oc nlb-dns ls --cluster <cluster_name_or_id>
    ```
    {: pre}

    In this example output, the `mycluster-a1b2cdef345678g9hi012j3kl4567890-i002.us-south.containers.appdomain.cloud` subdomain has the highest `i00<n>` value of `i002`.
    ```sh
    Subdomain                                                                               Load Balancer Hostname                        Health Monitor   SSL Cert Status           SSL Cert Secret Name
    mycluster-a1b2cdef345678g9hi012j3kl4567890-i000.us-south.containers.appdomain.cloud     ["1234abcd-us-south.lb.appdomain.cloud"]      None             created                   mycluster-a1b2cdef345678g9hi012j3kl4567890-i000
    mycluster-a1b2cdef345678g9hi012j3kl4567890-i001.us-south.containers.appdomain.cloud     ["5678efgh-us-south.lb.appdomain.cloud"]      None             created                   mycluster-a1b2cdef345678g9hi012j3kl4567890-i001
    mycluster-a1b2cdef345678g9hi012j3kl4567890-i002.us-south.containers.appdomain.cloud     ["9012ijkl-us-south.lb.appdomain.cloud"]      None             created                   mycluster-a1b2cdef345678g9hi012j3kl4567890-i002
    ```
    {: screen}

2. In the subdomain that you copied, change the `i00<n>` value in the subdomain to `000<n+1>`. For example, the `mycluster-a1b2cdef345678g9hi012j3kl4567890-i002.us-south.containers.appdomain.cloud` subdomain is changed to `mycluster-a1b2cdef345678g9hi012j3kl4567890-0003.us-south.containers.appdomain.cloud`. The `0` value indicates a public subdomain, and the `n+1` value indicates the next consecutive subdomain that you create in this cluster. You register this subdomain in later steps. When you register the domain, a TLS secret for the domain is automatically generated. The secret name follows a truncated format of the subdomain, such as `mycluster-a1b2cdef345678g9hi012j3kl4567890-0003`.


### Step 3: Create and configure a public Ingress controller
{: #ingress-public-vpc-3}

After you get your domain and TLS certificate ready, you must create a public Ingress controller and configure the controller with your domain.
{: shortdesc}

1. Create a configuration file for a public Ingress controller.
    ```yaml
    apiVersion: operator.openshift.io/v1
    kind: IngressController
    metadata:
      name: public-ingress-controller
      namespace: openshift-ingress-operator
    spec:
      replicas: 2
      domain: <domain>
      endpointPublishingStrategy:
        loadBalancer:
          scope: External
        type: LoadBalancerService
    ```
    {: codeblock}

2. Create the IngressController resource in the `openshift-ingress-operator` project of your cluster. When you create the IngressController, a public Ingress controller is automatically created and deployed in the `openshift-ingress` project based on the IngressController settings. Additionally, a Ingress controller service is created to expose the Ingress controller.
    ```sh
    oc create -f public-ingress-controller.yaml -n openshift-ingress-operator
    ```
    {: pre}

3. Run the **`oc get`** command and find the VPC hostname in the **EXTERNAL IP** field of the `router-public-ingress-controller` service. In VPC clusters, services' external IP addresses are non-static, and are instead kept behind a VPC-assigned hostname.
    ```sh
    oc get svc router-public-ingress-controller -n openshift-ingress
    ```
    {: pre}

    Example output

    ```sh
    NAME                                  TYPE           CLUSTER-IP       EXTERNAL-IP                             PORT(S)                      AGE
    router-public-ingress-controller     LoadBalancer   172.21.57.132    1234abcd-us-south.lb.appdomain.cloud    80/TCP,443/TCP,1940/TCP      3m
    ```
    {: screen}

4. Register the service's VPC hostname with the domain you previously chose.
    * Custom domain: Work with your DNS provider to add the `router-public-ingress-controller` service's VPC hostname as a CNAME that maps to your custom domain.
    * IBM-provided domain: Create a DNS entry for the `router-public-ingress-controller` service's VPC hostname. When you run the following command, the subdomain that you specified in the `public-ingress-controller.yaml` file is automatically generated, and is registered with the `router-public-ingress-controller` service. A TLS secret for the domain is automatically generated in the project that you specify where your app runs. The secret name follows a truncated format of the subdomain, such as `mycluster-a1b2cdef345678g9hi012j3kl4567890-0003`.
        ```sh
        ibmcloud oc nlb-dns create vpc-gen2 --cluster <cluster_name_or_ID> --lb-host <VPC_hostname> --type public --secret-namespace <project>
        ```
        {: pre}


### Step 4: Create the Ingress resource
{: #ingress-public-vpc-4}

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
    :    Replace `<domain>` with your subdomain. If your cluster has multiple projects where apps are exposed, one Ingress resource is required per project. You can use the same subdomain in each resource or different subdomains in each resource. For example, if you use a wildcard domain, you can append a wildcard subdomain to the beginning of the domain, such as `subdomain1.custom_domain.net`. Do not use &ast; for your host or leave the host property empty to avoid failures during Ingress creation.

    `path`
    :    Replace `<app_path>` with the path that your app is listening on. The path is appended to the IBM-provided or your custom domain to create a unique route to your app. When you enter this route into a web browser, network traffic is routed to the Ingress controller. The Ingress controller looks up the associated service, and sends network traffic to the service. The service then forwards the traffic to the pods where the app runs. Many apps don't listen on a specific path, but use the root path and a specific port. In this case, define the root path as `/` and don't specify an individual path for your app.
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



### Step 5: Access your app from the internet
{: #ingress-public-vpc-5}

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


## Publicly exposing apps that are outside your cluster
{: #ingress-roks4-external}

Expose apps that are outside your cluster to the public by including them in public Ingress load balancing. Incoming public requests on the IBM-provided or your custom domain are forwarded automatically to the external app.
{: shortdesc}

Before you begin, ensure that the external app that you want to include into the cluster load balancing can be accessed by using a public IP address.
{: note}

To expose apps that are outside of your cluster to the public, follow these steps.
1. Define a Kubernetes service configuration file for the app that the Ingress controller exposes. This service forwards incoming requests to an external endpoint that you create in subsequent steps.
    ```yaml
    apiVersion: v1
    kind: Service
    metadata:
      name: myexternalservice
    spec:
      ports:
       - protocol: TCP
         port: <app_port>
    ```
    {: codeblock}

2. Create the service in your cluster.
    ```sh
    oc apply -f myexternalservice.yaml
    ```
    {: pre}

3. Define an external endpoint configuration file. Include all public IP addresses and ports that you can use to access your external app. Note that the name of the endpoint must be the same as the name of the service that you created in the previous step, for example, `myexternalservice`.
    ```yaml
    kind: Endpoints
    apiVersion: v1
    metadata:
      name: myexternalservice
    subsets:
      - addresses:
          - ip: <external_IP1>
          - ip: <external_IP2>
        ports:
          - port: <external_port>
    ```
    {: codeblock}

    `name`
    :    Replace `<myexternalendpoint>` with the name of the Kubernetes service that you created earlier.

    `ip`
    :    Replace `<external_IP>` with the public IP addresses to connect to your external app.

    `port`
    :    Replace `<external_port>` with the port that your external app listens to.

4. Create the endpoint in your cluster.
    ```sh
    oc apply -f myexternalendpoint.yaml
    ```
    {: pre}

5. Continue with the second step in [Publicly exposing apps in VPC clusters with a private cloud service endpoint only](#ingress-public-expose-vpc-private-se) or [Publicly exposing apps in clusters with a public cloud service endpoint](#ingress-public-se).


