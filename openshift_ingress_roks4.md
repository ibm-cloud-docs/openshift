---

copyright:
  years: 2014, 2022
lastupdated: "2022-06-15"

keywords: openshift, nginx, ingress controller

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}




# Setting up Ingress
{: #ingress-roks4}

Expose multiple apps in your {{site.data.keyword.openshiftlong}} cluster by creating Ingress resources that are managed by the Ingress controller.
{: shortdesc}

![Version 4 icon.](images/icon-version-43.png) This information is for clusters that run {{site.data.keyword.redhat_openshift_notm}} version 4 only.
{: note}

For information about how to expose apps in {{site.data.keyword.satelliteshort}}, see Exposing apps in {{site.data.keyword.satelliteshort}} clusters](/docs/openshift?topic=openshift-sat-expose-apps).
{: tip}

## Prerequisites
{: #ingress-roks4-prereqs}

Before you get started with Ingress, review the following prerequisites.
{: shortdesc}

- Setting up Ingress requires the following [{{site.data.keyword.cloud_notm}} IAM roles](/docs/openshift?topic=openshift-users):
    - **Administrator** platform access role for the cluster in {{site.data.keyword.containerlong_notm}}
    - **Manager** service access role in all {{site.data.keyword.containerlong_notm}} namespaces ({{site.data.keyword.redhat_openshift_notm}} projects)
- If a zone fails, you might see intermittent failures in requests to apps that are exposed by the Ingress controller in that zone.
- To ensure high availability, at least two worker nodes per zone are recommended.
* ![VPC](../icons/vpc.svg "VPC") VPC clusters: [Allow traffic requests that are routed by Ingress to node ports on your worker nodes](/docs/openshift?topic=openshift-vpc-security-group).
* ![VPC](../icons/vpc.svg "VPC") VPC multizone clusters: If you created a cluster in the CLI and later manually added zones to your worker pools with the `ibmcloud oc zone add vpc-gen2` command, you must [update the VPC load balancer that exposes the Ingress controller](/docs/openshift?topic=openshift-router-mzr-error) to include subnets for all zones in your cluster.
* ![Classic](../icons/classic.svg "Classic") Classic clusters: Enable a [Virtual Router Function (VRF)](/docs/account?topic=account-vrf-service-endpoint#vrf) for your IBM Cloud infrastructure account. To enable VRF, see [Enabling VRF](/docs/account?topic=account-vrf-service-endpoint#vrf). To check whether a VRF is already enabled, use the `ibmcloud account show` command. If you can't or don't want to enable VRF, enable [VLAN spanning](/docs/vlans?topic=vlans-vlan-spanning#vlan-spanning). When a VRF or VLAN spanning is enabled, the Ingress controller can route packets to various subnets in the account.



## Planning networking for single or multiple projects
{: #multiple_projects}

One Ingress resource is required per project where you have apps that you want to expose.
{: shortdesc}

### All apps are in one project
{: #one-project}

If the apps in your cluster are all in the same project, you must create one Ingress resource to define the routing rules for the apps that you want to expose.
{: shortdesc}

For example, if you have `app1` and `app2` exposed by services in a development project, you can create an Ingress resource in the project. The resource specifies `domain.net` as the host and registers the paths that each app listens on with `domain.net`.

![One resource is required per project](images/cs_ingress_single_ns.png)

Note that if you want to use different domains for the apps within the same project, you can create one resource per domain.

### Apps are in multiple projects
{: #multi-project}

If the apps in your cluster are in different projects, you must create one Ingress resource for each project to define the app's routing rules.
{: shortdesc}

You can either define the same domain in multiple resources, or use a wildcard domain to specify different subdomains within the Ingress resource for each project.


When a wildcard domain is registered, multiple subdomains can all resolve to the same host. The IBM-provided Ingress subdomain wildcard, `*.<cluster_name>.<globally_unique_account_HASH>-0000.<region>.containers.appdomain.cloud`, is registered by default for your cluster.{: #wildcard_tls}

The IBM-provided TLS certificate is a wildcard certificate and can be used for the wildcard subdomain. If you want to use a wildcard custom domain, you must register the custom domain as a wildcard domain such as `*.custom_domain.net`, and to use TLS, you must get a wildcard certificate.
{: note}

For example, consider the following scenario in which you might want to use a wildcard subdomain:
* You have two versions of the same app, `app1` and `app3`, for testing purposes.
* You deploy the apps in two different projects within the same cluster: `app1` into the development project, and `app3` into the staging project.

To use different subdomains to manage traffic to these apps, you create the following services and resources:
* A Kubernetes service in the development project to expose `app1`.
* An Ingress resource in the development project that specifies the host as `dev.domain.net`.
* A Kubernetes service in the staging project to expose `app3`.
* An Ingress resource in the staging project that specifies the host as `stage.domain.net`.

![Within a project, use subdomains in one or multiple resources](images/cs_ingress_multi_ns.png)

Now, both URLs resolve to the same domain. However, because the resource in the staging project is registered with the `stage` subdomain, the Ingress controller correctly proxies requests from the `stage.domain.net/app3` URL to only `app3`.

### Multiple domains within a project
{: #multi-domains-project}

Within an individual project, you can use one domain to access all the apps in the project. If you want to use different domains for the apps within an individual project, use a wildcard domain. When a wildcard domain is registered, multiple subdomains all resolve to the same host. Then, you can use one resource to specify multiple subdomain hosts within that resource. Alternatively, you can create multiple Ingress resources in the project and specify a different subdomain in each Ingress resource.
{: shortdesc}

![One resource is required per project](images/cs_ingress_single_ns_multi_subs.png)

The IBM-provided Ingress subdomain wildcard, `*.<cluster_name>.<globally_unique_account_HASH>-0000.<region>.containers.appdomain.cloud`, is registered by default for your cluster. The IBM-provided TLS certificate is a wildcard certificate and can be used for the wildcard subdomain. If you want to use a wildcard custom domain, you must register the custom domain as a wildcard domain such as `*.custom_domain.net`, and to use TLS, you must get a wildcard certificate.
{: note}



## Publicly exposing apps in classic clusters or in VPC clusters with a public cloud service endpoint
{: #ingress-roks4-public}

If your cluster is created on ![Classic](../icons/classic.svg "Classic") classic infrastructure, or if your cluster is created on ![VPC](../icons/vpc.svg "VPC") VPC infrastructure and you enabled the public cloud service endpoint during cluster creation, you can use the default public Ingress controller to expose apps in your cluster to receive requests that are from the public network.
{: shortdesc}

**Before you begin**:
* Review the Ingress [prerequisites](#ingress-roks4-prereqs).
* [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

### Step 1: Deploy apps and create app services
{: #ingress-roks4-public-1}

Start by deploying your apps and creating Kubernetes services to expose them.
{: shortdesc}

1. [Deploy your app to the cluster](/docs/openshift?topic=openshift-openshift_apps). Ensure that you add a label to your deployment in the metadata section of your configuration file, such as `app: code`. This label is needed to identify all pods where your app runs so that the pods are in the Ingress load balancing.

2. For each app deployment that you want to expose, create a Kubernetes `ClusterIP` service. Your app must be exposed by a Kubernetes service to be included in the Ingress load balancing.

    ```sh
    oc expose deploy <app_deployment_name> --name my-app-svc --port <app_port> -n <namespace>
    ```
    {: pre}
    



### Step 2: Select an app domain and TLS termination
{: #ingress-roks4-public-2}

Choose the domain that you use to access your apps and the TLS termination for the app.
{: shortdesc}

You can use the IBM-provided domain, such as `mycluster-<hash>-0000.us-south.containers.appdomain.cloud/myapp`, to access your app from the internet. To use a custom domain instead, you can set up a CNAME record to map your custom domain to the IBM-provided domain.

The Ingress controller load balances HTTP network traffic to the apps in your cluster. To load balance incoming HTTPS connections, you can use a TLS certificate so that the Ingress controller can decrypt the network traffic and forward the decrypted request to the apps that are exposed in your cluster.

Currently, when you configure TLS termination for Ingress, only HTTPS connections are permitted.
{: note}

For more information about TLS certificates, see [Managing TLS certificates and secrets](#manage_certs).

**To use the IBM-provided Ingress domain and TLS secret:**

1. Get the IBM-provided domain and secret to use in subsequent steps. The IBM-provided TLS certificate is stored as the `Ingress secret` in the `openshift-ingress` project.
    ```sh
    ibmcloud oc cluster get --cluster <cluster_name_or_ID> | grep Ingress
    ```
    {: pre}

    Example output

    ```sh
    Ingress Subdomain:      mycluster-<hash>-0000.us-south.containers.appdomain.cloud
    Ingress Secret:         mycluster-<hash>-0000
    ```
    {: screen}

2. The Ingress controller can access TLS secrets only in the same project that the Ingress resource is deployed to. If your app is deployed in a project other than `openshift-ingress`, you must copy the default TLS secret from `openshift-ingress` to that project.
    1. Get the CRN of the secret for your subdomain.
        ```sh
        ibmcloud oc ingress secret get -c <cluster> --name <secret_name> --namespace openshift-ingress
        ```
        {: pre}

    2. Using the CRN, create a secret for the certificate in the project where your app is deployed.
        ```sh
        ibmcloud oc ingress secret create --cluster <cluster_name_or_ID> --cert-crn <CRN> --name <secret_name> --namespace project
        ```
        {: pre}

**To use a custom domain and TLS secret:**

1. Prepare your custom domain.
    1. Work with your Domain Name Service (DNS) provider or [{{site.data.keyword.cloud_notm}} DNS](/docs/dns?topic=dns-getting-started) to register your custom domain. If you want to use different subdomains for your apps, register the custom domain as a wildcard domain, such as `*.custom_domain.net`. Note that domains are limited to 255 characters or fewer in {{site.data.keyword.redhat_openshift_notm}} version 4.5 or earlier, and 130 characters or fewer in {{site.data.keyword.redhat_openshift_notm}} version 4.6 or later.
    2. Define an alias for your custom domain by specifying the IBM-provided domain as a Canonical Name record (CNAME). To find the IBM-provided Ingress domain, run `ibmcloud oc cluster get --cluster <cluster_name>` and look for the **Ingress subdomain** field.

2. If you want to configure TLS termination, prepare your custom TLS secret.
    * To use a TLS certificate that is stored in {{site.data.keyword.cloudcerts_long_notm}}, create a secret for the certificate in the same project as your app.
        Do not create the secret with the same name as the IBM-provided Ingress secret, which you can find by running `ibmcloud oc cluster get --cluster <cluster_name_or_ID> | grep Ingress`.
        {: note}

        ```sh
        ibmcloud oc ingress secret create --name <secret_name> --cluster <cluster_name_or_ID> --cert-crn <certificate_crn> --namespace <project>
        ```
        {: pre}

    * To create a TLS certificate:
        1. Generate a certificate authority (CA) cert and key from your certificate provider.
          * If you have your own domain, purchase an official TLS certificate for your domain.
          * Make sure the [CN](https://support.dnsimple.com/articles/what-is-common-name/){: external} is different for each certificate.
          * If you registered a wildcard domain, generate a wildcard certificate.
          * TLS certificates that contain pre-shared keys (TLS-PSK) are not supported.
        2. Encode the cert and key into base64 and save the base64 encoded value in a new file.
            ```sh
            openssl base64 -in tls.key -out tls.key.base64
            ```
            {: pre}

        3. View the base64 encoded value for your cert and key.
            ```sh
            cat tls.key.base64
            ```
            {: pre}

        4. Create a Kubernetes secret for your certificate in the project where your app services are deployed. Do not create the secret with the same name as the IBM-provided Ingress secret, which you can find by running `ibmcloud oc cluster get --cluster <cluster_name_or_ID> | grep Ingress`.
            ```sh
            oc create secret tls <secret_name> -n <project> --cert=<tls.crt> --key=<tls.key>
            ```
            {: pre}

### Step 3: Create the Ingress resource
{: #ingress-roks4-public-3}

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
        - <domain>
        secretName: <secret_name>
      rules:
      - host: <domain>
        http:
          paths:
          - path: /<app1_path>
            backend:
              serviceName: <app1_service>
              servicePort: 80
          - path: /<app2_path>
            backend:
              serviceName: <app2_service>
              servicePort: 80
    ```
    {: codeblock}



    `tls`
    :    If you want to use TLS, include this TLS section in your resource. Replace `<domain>` with your subdomain. Do not use `*` for your host or leave the host property empty to avoid failures during Ingress creation. Replace `<tls_secret_name>` with the secret that you created earlier that holds your TLS certificate and key for a custom domain or the TLS secret that was automatically generated for an IBM-provided subdomain.

    `host`
    :    Replace `<domain>` with the IBM-provided Ingress subdomain or your custom domain. If your cluster has multiple projects where apps are exposed, one Ingress resource is required per project. You can use the same subdomain in each resource or different subdomains in each resource. For example, if you use a wildcard domain, you can append a wildcard subdomain to the beginning of the domain, such as `subdomain1.custom_domain.net` or `subdomain1.mycluster-<hash>-0000.us-south.containers.appdomain.cloud`. Do not use &ast; for your host or leave the host property empty to avoid failures during Ingress creation.

    `path`
    :    Replace `<app_path>` with a slash or the path that your app is listening on. The path is appended to the IBM-provided or your custom domain to create a unique route to your app. When you enter this route into a web browser, network traffic is routed to the Ingress controller. The Ingress controller looks up the associated service, and the Ingress controller sends network traffic to the service. The service then forwards the traffic to the pods where the app runs. Many apps don't listen on a specific path, but use the root path and a specific port. In this case, define the root path as `/` and don't specify an individual path for your app. For `http://domain/`, enter `/` as the path. For `http://domain/app1_path`, enter `/app1_path` as the path.

    `serviceName`
    :    Replace `<app1_service>` and `<app2_service>`, and so on, with the name of the services you created to expose your apps. If your apps are exposed by services in different projects in the cluster, include only app services that are in the same project. You must create one Ingress resource for each project where you have apps that you want to expose.

    `servicePort`
    :    The port that your service listens to. Use the same port that you defined when you created the Kubernetes service for your app.



2. Create the Ingress resource for your cluster. Ensure that the resource deploys into the same project as the app services that you specified in the resource.
    ```sh
    oc apply -f myingressresource.yaml -n <project>
    ```
    {: pre}

3. Verify that the Ingress resource was created successfully. If messages in the events describe an error in your resource configuration, change the values in your resource file and reapply the file for the resource.
    ```sh
    oc describe ingress myingressresource
    ```
    {: pre}


Your Ingress resource is created in the same project as your app services, and your apps are registered with the Ingress controller.

### Step 4: Access your app from the internet
{: #ingress-roks4-public-4}

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

Having trouble connecting to your app through Ingress? Try [Troubleshooting Ingress](/docs/openshift?topic=openshift-ingress-status).
{: tip}



## Publicly exposing apps in VPC clusters with a private cloud service endpoint only
{: #priv-se-pub-controller}

![VPC](../icons/vpc.svg "VPC") If your cluster is created on VPC infrastructure and you enabled only the private cloud service endpoint during cluster creation, your cluster is created with only a private Ingress controller by default. To publicly expose your apps, you must first create a public Ingress controller. Then, you must register your Ingress controller with a subdomain and, optionally, import your own TLS certificate.
{: shortdesc}

**Before you begin**:
* Review the Ingress [prerequisites](#ingress-roks4-prereqs).
* [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

### Step 1: Deploy apps and create app services
{: #priv-se-pub-controller-1}

Start by deploying your apps and creating Kubernetes services to expose them.
{: shortdesc}

1. [Deploy your app to the cluster](/docs/openshift?topic=openshift-openshift_apps). Ensure that you add a label to your deployment in the metadata section of your configuration file, such as `app: code`. This label is needed to identify all pods where your app runs so that the pods are in the Ingress load balancing.

2. For each app deployment that you want to expose, create a Kubernetes `ClusterIP` service. Your app must be exposed by a Kubernetes service to be included in the Ingress load balancing.

    ```sh
    oc expose deploy <app_deployment_name> --name my-app-svc --port <app_port> -n <namespace>
    ```
    {: pre}
    



### Step 2: Register a subdomain and TLS certificate
{: #priv-se-pub-controller-2}

When you configure the public Ingress controller, you must expose your app by using a custom or an IBM-provided domain.
{: shortdesc}

The Ingress controller load balances HTTP network traffic to the apps in your cluster. To load balance incoming HTTPS connections, you can add a TLS certificate to your Ingress resource in the next section so that the Ingress controller can decrypt the network traffic and forward the decrypted request to the apps that are exposed in your cluster.

Currently, when you configure TLS termination for Ingress, only HTTPS connections are permitted.
{: note}

**Custom domain and TLS secret**:

1. Register a custom domain by working with your Domain Name Service (DNS) provider or [{{site.data.keyword.cloud_notm}} DNS](/docs/dns?topic=dns-getting-started). Note that domains are limited to 255 characters or fewer in {{site.data.keyword.redhat_openshift_notm}} version 4.5 or earlier, and 130 characters or fewer in {{site.data.keyword.redhat_openshift_notm}} version 4.6 or later.
    If you want to use the same subdomain for multiple services in your cluster, you can register a wildcard subdomain, such as `*.example.com`.
    {: tip}

2. If you want to configure TLS termination, prepare your custom TLS secret.
    * To use a TLS certificate that is stored in {{site.data.keyword.cloudcerts_long_notm}}, create a secret for the certificate in the same project as your app.
        Do not create the secret with the same name as the IBM-provided Ingress secret, which you can find by running `ibmcloud oc cluster get --cluster <cluster_name_or_ID> | grep Ingress`.
        {: note}

        ```sh
        ibmcloud oc ingress secret create --name <secret_name> --cluster <cluster_name_or_ID> --cert-crn <certificate_crn> --namespace <project>
        ```
        {: pre}

    * To create a TLS certificate:
        1. Generate a certificate authority (CA) cert and key from your certificate provider.
          * If you have your own domain, purchase an official TLS certificate for your domain.
          * Make sure the [CN](https://support.dnsimple.com/articles/what-is-common-name/){: external} is different for each certificate.
          * If you registered a wildcard domain, generate a wildcard certificate.
          * TLS certificates that contain pre-shared keys (TLS-PSK) are not supported.
        2. Convert the cert and key into base64.
            1. Encode the cert and key into base64 and save the base64 encoded value in a new file.
                ```sh
                openssl base64 -in tls.key -out tls.key.base64
                ```
                {: pre}

            2. View the base64 encoded value for your cert and key.
                ```sh
                cat tls.key.base64
                ```
                {: pre}

        3. Create a Kubernetes secret for your certificate in the project where your app services are deployed.
            ```sh
            oc create secret tls <secret_name> -n <project> --cert=<tls.crt> --key=<tls.key>
            ```
            {: pre}

            Do not create the secret with the same name as the IBM-provided Ingress secret, which you can find by running `ibmcloud oc cluster get --cluster <cluster_name_or_ID> | grep Ingress`.
            {: note}

**IBM-provided domain and TLS secret**:

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

2. In the subdomain that you copied, change the `i00<n>` value in the subdomain to `000<n+1>`. For example, the `mycluster-a1b2cdef345678g9hi012j3kl4567890-i002.us-south.containers.appdomain.cloud` subdomain is changed to `mycluster-a1b2cdef345678g9hi012j3kl4567890-0003.us-south.containers.appdomain.cloud`. The `0` value indicates a public subdomain, and the `n+1` value indicates the next consecutive subdomain that you create in this cluster. You register this subdomain in later steps. When you register the domain in subsequent steps, a TLS secret for the domain is automatically generated. The secret name follows a truncated format of the subdomain, such as `mycluster-a1b2cdef345678g9hi012j3kl4567890-0003`.



### Step 3: Create and configure a public Ingress controller
{: #priv-se-pub-controller-3}

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

3. Get the VPC hostname in the **EXTERNAL IP** field of the `router-public-ingress-controller` service. In VPC clusters, services' external IP addresses are non-static, and are instead kept behind a VPC-assigned hostname.
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
{: #priv-se-pub-controller-4}

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
              serviceName: <app1_service>
              servicePort: 80
          - path: /<app2_path>
            backend:
              serviceName: <app2_service>
              servicePort: 80
    ```
    {: codeblock}

    `tls`
    :    If you want to use TLS, include this TLS section in your resource with the following fields.
    :    Replace `<domain>` with your subdomain. Do not use &ast; for your host or leave the host property empty to avoid failures during Ingress creation.
    :    Replace `<tls_secret_name>` with the secret that you created earlier that holds your TLS certificate and key for a custom domain or the TLS secret that was automatically generated for an IBM-provided subdomain.

    `host`
    :    Replace `<domain>` with your subdomain. If your cluster has multiple projects where apps are exposed, one Ingress resource is required per project. You can use the same subdomain in each resource or different subdomains in each resource. For example, if you use a wildcard domain, you can append a wildcard subdomain to the beginning of the domain, such as `subdomain1.custom_domain.net`. Do not use &ast; for your host or leave the host property empty to avoid failures during Ingress creation.

    `path`
    :    Replace `<app_path>` with a slash or the path that your app is listening on. The path is appended to the IBM-provided or your custom domain to create a unique route to your app. When you enter this route into a web browser, network traffic is routed to the Ingress controller. The Ingress controller looks up the associated service, and sends network traffic to the service. The service then forwards the traffic to the pods where the app runs. Many apps don't listen on a specific path, but use the root path and a specific port. In this case, define the root path as `/` and don't specify an individual path for your app.
    :    Examples: For `http://domain/`, enter `/` as the path. For `http://domain/app1_path`, enter `/app1_path` as the path.

    `serviceName`
    :    Replace `<app1_service>` and `<app2_service>`, and so on, with the name of the services you created to expose your apps. If your apps are exposed by services in different projects in the cluster, include only app services that are in the same project. You must create one Ingress resource for each project where you have apps that you want to expose.

    `servicePort`
    :    The port that your service listens to. Use the same port that you defined when you created the Kubernetes service for your app.



2. Create the Ingress resource for your cluster. Ensure that the resource deploys into the same project as the app services that you specified in the resource.
    ```sh
    oc apply -f myingressresource.yaml -n <project>
    ```
    {: pre}

3. Verify that the Ingress resource was created successfully. If messages in the events describe an error in your resource configuration, change the values in your resource file and reapply the file for the resource.
    ```sh
    oc describe ingress myingressresource
    ```
    {: pre}

Your Ingress resource is created in the same project as your app services, and your apps are registered with the Ingress controller.



### Step 5: Access your app from the internet
{: #priv-se-pub-controller-5}

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

Having trouble connecting to your app through Ingress? Try [Troubleshooting Ingress](/docs/openshift?topic=openshift-ingress-status).
{: tip}



## Publicly exposing apps that are outside your cluster
{: #ingress-roks4-external}

Expose apps that are outside your cluster to the public by including them in public Ingress load balancing. Incoming public requests on the IBM-provided or your custom domain are forwarded automatically to the external app.
{: shortdesc}

**Before you begin**:
* Review the Ingress [prerequisites](#ingress-roks4-prereqs).
* Ensure that the external app that you want to include into the cluster load balancing can be accessed by using a public IP address.
* [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

To expose apps that are outside of your cluster to the public:
1. Define a Kubernetes service configuration file for the app that the Ingress controller will expose. This service that forwards incoming requests to an external endpoint that you create in subsequent steps.
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

3. Define an external endpoint configuration file. Include all public IP addresses and ports that you can use to access your external app. Note that the name of the endpoint must be the same as the name of the service that you defined in the previous step, `myexternalservice`.
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

5. Continue with the second step in [Exposing apps to the public in classic clusters or in VPC clusters with a public cloud service endpoint](#ingress-roks4-public-2) or [Exposing apps to the public in VPC clusters with a private cloud service endpoint only](#priv-se-pub-controller-2).



## Privately exposing apps in classic clusters or in VPC clusters with a public cloud service endpoint
{: #ingress-roks4-private}

If your cluster is created on ![Classic](../icons/classic.svg "Classic") classic infrastructure, or if your cluster is created on ![VPC](../icons/vpc.svg "VPC") VPC infrastructure and you enabled the public cloud service endpoint during cluster creation, your cluster is created with only a public Ingress controller by default. To privately expose your apps, you must first create a private Ingress controller. Then you must register your Ingress controller with a subdomain and, optionally, import your own TLS certificate.
{: shortdesc}

**Before you begin**:
* Review the Ingress [prerequisites](#ingress-roks4-prereqs).
* [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

### Step 1: Deploy apps and create app services
{: #ingress-roks4-private-1}

Start by deploying your apps and creating Kubernetes services to expose them.
{: shortdesc}

1. [Deploy your app to the cluster](/docs/openshift?topic=openshift-openshift_apps). Ensure that you add a label to your deployment in the metadata section of your configuration file, such as `app: code`. This label is needed to identify all pods where your app runs so that the pods are in the Ingress load balancing.

2. For each app deployment that you want to expose, create a Kubernetes `ClusterIP` service. Your app must be exposed by a Kubernetes service to be included in the Ingress load balancing.

    ```sh
    oc expose deploy <app_deployment_name> --name my-app-svc --port <app_port> -n <namespace>
    ```
    {: pre}
    



### Step 2: Register a subdomain and TLS certificate
{: #ingress-roks4-private-2}

When you configure the private Ingress controller, you must expose your app by using a custom or an IBM-provided domain.
{: shortdesc}

The Ingress controller load balances HTTP network traffic to the apps in your cluster. To load balance incoming HTTPS connections, you can add a TLS certificate to your Ingress resource in the next section so that the Ingress controller can decrypt the network traffic and forward the decrypted request to the apps that are exposed in your cluster.

Currently, when you configure TLS termination for Ingress, only HTTPS connections are permitted.
{: note}



**Custom domain and TLS secret, classic or VPC clusters**:

1. Register a custom domain by working with your Domain Name Service (DNS) provider or [{{site.data.keyword.cloud_notm}} DNS](/docs/dns?topic=dns-getting-started). Note that domains are limited to 255 characters or fewer in {{site.data.keyword.redhat_openshift_notm}} version 4.5 or earlier, and 130 characters or fewer in {{site.data.keyword.redhat_openshift_notm}} version 4.6 or later.
    If you want to use the same subdomain for multiple services in your cluster, you can register a wildcard subdomain, such as `*.example.com`.
    {: tip}


2. If you want to configure TLS termination, prepare your custom TLS secret.
    * To use a TLS certificate that is stored in {{site.data.keyword.cloudcerts_long_notm}}, create a secret for the certificate in the same project as your app.
        Do not create the secret with the same name as the IBM-provided Ingress secret, which you can find by running `ibmcloud oc cluster get --cluster <cluster_name_or_ID> | grep Ingress`.
        {: note}

        ```sh
        ibmcloud oc ingress secret create --name <secret_name> --cluster <cluster_name_or_ID> --cert-crn <certificate_crn> --namespace <project>
        ```
        {: pre}

    * To create a TLS certificate:
        1. Generate a certificate authority (CA) cert and key from your certificate provider.
          * If you have your own domain, purchase an official TLS certificate for your domain.
          * Make sure the [CN](https://support.dnsimple.com/articles/what-is-common-name/){: external} is different for each certificate.
          * If you registered a wildcard domain, generate a wildcard certificate.
          * TLS certificates that contain pre-shared keys (TLS-PSK) are not supported.
        2. Convert the cert and key into base64.
            1. Encode the cert and key into base64 and save the base64 encoded value in a new file.
                ```sh
                openssl base64 -in tls.key -out tls.key.base64
                ```
                {: pre}

            2. View the base64 encoded value for your cert and key.
                ```sh
                cat tls.key.base64
                ```
                {: pre}

        3. Create a Kubernetes secret for your certificate in the project where your app services are deployed.
            ```sh
            oc create secret tls <secret_name> -n <project> --cert=<tls.crt> --key=<tls.key>
            ```
            {: pre}

            Do not create the secret with the same name as the IBM-provided Ingress secret, which you can find by running `ibmcloud oc cluster get --cluster <cluster_name_or_ID> | grep Ingress`.
            {: note}

**IBM-provided domain and TLS secret, VPC clusters only**:

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

2. In the subdomain that you copied, change the `000<n>` value in the subdomain to `i00<n+1>`. For example, the `mycluster-a1b2cdef345678g9hi012j3kl4567890-0002.us-south.containers.appdomain.cloud` subdomain is changed to `mycluster-a1b2cdef345678g9hi012j3kl4567890-i003.us-south.containers.appdomain.cloud`. The `i` value indicates a private subdomain, and the `n+1` value indicates the next consecutive subdomain that you create in this cluster. You register this subdomain in later steps. When you register the domain in subsequent steps, a TLS secret for the domain is automatically generated. The secret name follows a truncated format of the subdomain, such as `mycluster-a1b2cdef345678g9hi012j3kl4567890-i003`.



### Step 3: Create and configure a private Ingress controller
{: #ingress-roks4-private-3}

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

2. Create the IngressController resource in the `openshift-ingress-operator` project of your cluster. When you create the IngressController, a private Ingress controller is automatically created and deployed in the `openshift-ingress` project based on the IngressController settings. Additionally, a Ingress controller service is created to expose the Ingress controller with an IP address (classic clusters) or a VPC hostname (VPC clusters).
    ```sh
    oc create -f private-ingress-controller.yaml -n openshift-ingress-operator
    ```
    {: pre}

3. Get the IP address or VPC hostname in the **EXTERNAL IP** field of the `router-private-ingress-controller` service.
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
{: #ingress-roks4-private-4}

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
              serviceName: <app1_service>
              servicePort: 80
          - path: /<app2_path>
            backend:
              serviceName: <app2_service>
              servicePort: 80
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
    :   Replace `<app_path>` with a slash or the path that your app is listening on. The path is appended to the IBM-provided or your custom domain to create a unique route to your app. When you enter this route into a web browser, network traffic is routed to the Ingress controller. The Ingress controller looks up the associated service, and sends network traffic to the service. The service then forwards the traffic to the pods where the app runs. Many apps don't listen on a specific path, but use the root path and a specific port. In this case, define the root path as `/` and don't specify an individual path for your app.
    :    Examples: For `http://domain/`, enter `/` as the path. For `http://domain/app1_path`, enter `/app1_path` as the path.

    `serviceName`
    :    Replace `<app1_service>` and `<app2_service>`, and so on, with the name of the services you created to expose your apps. If your apps are exposed by services in different projects in the cluster, include only app services that are in the same project. You must create one Ingress resource for each project where you have apps that you want to expose.

    `servicePort`
    :    The port that your service listens to. Use the same port that you defined when you created the Kubernetes service for your app.



2. Create the Ingress resource for your cluster. Ensure that the resource deploys into the same project as the app services that you specified in the resource.
    ```sh
    oc apply -f myingressresource.yaml -n <project>
    ```
    {: pre}

3. Verify that the Ingress resource was created successfully. If messages in the events describe an error in your resource configuration, change the values in your resource file and reapply the file for the resource.
    ```sh
    oc describe ingress myingressresource
    ```
    {: pre}

Your Ingress resource is created in the same project as your app services, and your apps are registered with the Ingress controller.



### Step 5: Access your app from your private network
{: #ingress-roks4-private-5}

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

Having trouble connecting to your app through Ingress? Try [Troubleshooting Ingress](/docs/openshift?topic=openshift-ingress-status).
{: tip}



## Privately exposing apps in VPC clusters with a private cloud service endpoint only
{: #priv-se-priv-controller}

If your cluster is created on ![VPC](../icons/vpc.svg "VPC") VPC infrastructure and you enabled the private cloud service endpoint only during cluster creation, you can use the default private Ingress controller to expose apps in your cluster to requests that are from the private network.
{: shortdesc}

**Before you begin**:
* Review the Ingress [prerequisites](#ingress-roks4-prereqs).
* [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

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
    

### Step 2: Select an app domain and TLS termination
{: #priv-se-priv-controller-2}

Choose the domain that you use to access your apps and the TLS termination for the app.
{: shortdesc}

You can use the IBM-provided domain, such as `mycluster-<hash>-i000.us-south.containers.appdomain.cloud/myapp`, to access your app from the internet. To use a custom domain instead, you can set up a CNAME record to map your custom domain to the IBM-provided domain.

The Ingress controller load balances HTTP network traffic to the apps in your cluster. To load balance incoming HTTPS connections, you can use a TLS certificate so that the Ingress controller can decrypt the network traffic and forward the decrypted request to the apps that are exposed in your cluster.

Currently, when you configure TLS termination for Ingress, only HTTPS connections are permitted.
{: note}

For more information about TLS certificates, see [Managing TLS certificates and secrets](#manage_certs).

**To use the IBM-provided Ingress domain and TLS secret:**

1. Get the IBM-provided domain and secret to use in subsequent steps. The IBM-provided TLS certificate is stored as the `Ingress secret` in the `openshift-ingress` project.
    ```sh
    ibmcloud oc cluster get --cluster <cluster_name_or_ID> | grep Ingress
    ```
    {: pre}

    Example output

    ```sh
    Ingress Subdomain:      mycluster-<hash>-0000.us-south.containers.appdomain.cloud
    Ingress Secret:         mycluster-<hash>-0000
    ```
    {: screen}

2. The Ingress controller can access TLS secrets only in the same project that the Ingress resource is deployed to. If your app is deployed in a project other than `openshift-ingress`, you must copy the default TLS secret from `openshift-ingress` to that project.
    1. Get the CRN of the secret for your subdomain.
        ```sh
        ibmcloud oc ingress secret get -c <cluster> --name <secret_name> --namespace openshift-ingress
        ```
        {: pre}

    2. Using the CRN, create a secret for the certificate in the project where your app is deployed.
        ```sh
        ibmcloud oc ingress secret create --cluster <cluster_name_or_ID> --cert-crn <CRN> --name <secret_name> --namespace project
        ```
        {: pre}

**To use a custom domain and TLS secret:**

1. Prepare your custom domain.
    1. Work with your Domain Name Service (DNS) provider or [{{site.data.keyword.cloud_notm}} DNS](/docs/dns?topic=dns-getting-started) to register your custom domain. If you want to use different subdomains for your apps, register the custom domain as a wildcard domain, such as `*.custom_domain.net`. Note that domains are limited to 255 characters or fewer in {{site.data.keyword.redhat_openshift_notm}} version 4.5 or earlier, and 130 characters or fewer in {{site.data.keyword.redhat_openshift_notm}} version 4.6 or later.
    2. Define an alias for your custom domain by specifying the IBM-provided domain as a Canonical Name record (CNAME). To find the IBM-provided Ingress domain, run `ibmcloud oc cluster get --cluster <cluster_name>` and look for the **Ingress subdomain** field.

2. If you want to configure TLS termination, prepare your custom TLS secret.
    * To use a TLS certificate that is stored in {{site.data.keyword.cloudcerts_long_notm}}, create a secret for the certificate in the same project as your app.
        Do not create the secret with the same name as the IBM-provided Ingress secret, which you can find by running `ibmcloud oc cluster get --cluster <cluster_name_or_ID> | grep Ingress`.
        {: note}

        ```sh
        ibmcloud oc ingress secret create --name <secret_name> --cluster <cluster_name_or_ID> --cert-crn <certificate_crn> --namespace <project>
        ```
        {: pre}

    * To create a TLS certificate:
        1. Generate a certificate authority (CA) cert and key from your certificate provider.
            * If you have your own domain, purchase an official TLS certificate for your domain.
            * Make sure the [CN](https://support.dnsimple.com/articles/what-is-common-name/){: external} is different for each certificate.
            * If you registered a wildcard domain, generate a wildcard certificate.
            * TLS certificates that contain pre-shared keys (TLS-PSK) are not supported.
        2. Encode the cert and key into base64 and save the base64 encoded value in a new file.
            ```sh
            openssl base64 -in tls.key -out tls.key.base64
            ```
            {: pre}

        3. View the base64 encoded value for your cert and key.
            ```sh
            cat tls.key.base64
            ```
            {: pre}

        4. Create a Kubernetes secret for your certificate in the project where your app services are deployed. Do not create the secret with the same name as the IBM-provided Ingress secret, which you can find by running `ibmcloud oc cluster get --cluster <cluster_name_or_ID> | grep Ingress`.
            ```sh
            oc create secret tls <secret_name> -n <project> --cert=<tls.crt> --key=<tls.key>
            ```
            {: pre}

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
              serviceName: <app1_service>
              servicePort: 80
          - path: /<app2_path>
            backend:
              serviceName: <app2_service>
              servicePort: 80
    ```
    {: codeblock}


    `tls`
    :    If you want to use TLS, include this TLS section in your resource with the following fields.
    :    Replace `<domain>` with your subdomain. Do not use &ast; for your host or leave the host property empty to avoid failures during Ingress creation.
    :    Replace <tls_secret_name> with the secret that you created earlier that holds your TLS certificate and key for a custom domain or the TLS secret that was automatically generated for an IBM-provided subdomain.

    `host`
    :    Replace `<domain>` with the IBM-provided Ingress subdomain or your custom domain.
    :    If your cluster has multiple projects where apps are exposed, one Ingress resource is required per project. You can use the same subdomain in each resource or different subdomains in each resource. For example, if you use a wildcard domain, you can append a wildcard subdomain to the beginning of the domain, such as `subdomain1.custom_domain.net` or `subdomain1.mycluster-<hash>-0000.us-south.containers.appdomain.cloud`. Do not use`*` for your host or leave the host property empty to avoid failures during Ingress creation.

    `path`
    :   Replace `<app_path>` with a slash or the path that your app is listening on. The path is appended to the IBM-provided or your custom domain to create a unique route to your app. When you enter this route into a web browser, network traffic is routed to the Ingress controller. The Ingress controller looks up the associated service, and sends network traffic to the service. The service then forwards the traffic to the pods where the app runs. Many apps don't listen on a specific path, but use the root path and a specific port. In this case, define the root path as `/` and don't specify an individual path for your app.
    :    Examples: For `http://domain/`, enter `/` as the path. For `http://domain/app1_path`, enter `/app1_path` as the path.

    `serviceName`
    :    Replace `<app1_service>` and `<app2_service>`, and so on, with the name of the services you created to expose your apps. If your apps are exposed by services in different projects in the cluster, include only app services that are in the same project. You must create one Ingress resource for each project where you have apps that you want to expose.

    `servicePort`
    :    The port that your service listens to. Use the same port that you defined when you created the Kubernetes service for your app.



2. Create the Ingress resource for your cluster. Ensure that the resource deploys into the same project as the app services that you specified in the resource.
    ```sh
    oc apply -f myingressresource.yaml -n <project>
    ```
    {: pre}

3. Verify that the Ingress resource was created successfully. If messages in the events describe an error in your resource configuration, change the values in your resource file and reapply the file for the resource.
    ```sh
    oc describe ingress myingressresource
    ```
    {: pre}

Your Ingress resource is created in the same project as your app services, and your apps are registered with the Ingress controller.



### Step 4: Access your app from the internet
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

Having trouble connecting to your app through Ingress? Try [Troubleshooting Ingress](/docs/openshift?topic=openshift-ingress-status).
{: tip}

## Managing TLS certificates and secrets
{: #manage_certs}

As of 24 August 2020, an [{{site.data.keyword.cloudcerts_long}}](/docs/certificate-manager?topic=certificate-manager-about-certificate-manager) instance is automatically created for each cluster that you can use to manage the cluster's Ingress TLS certificates.
{: shortdesc}

{{site.data.keyword.cloudcerts_short}} is deprecated. Automatic provisioning of {{site.data.keyword.cloudcerts_short}} instances in new clusters ends on 23 September 2022. Support for {{site.data.keyword.cloudcerts_short}} ends on 1 December 2022 and any remaining {{site.data.keyword.cloudcerts_short}} instances are set to be deleted on 31 Dec 2022. After this date, certificates are set to be written only to the cluster unless you set up a Secrets Manager instance. Migrate your certificates to IBM Cloud Secrets Manager as soon as possible.
{: deprecated}

For a {{site.data.keyword.cloudcerts_short}} instance to be created for your new or existing cluster, ensure that the API key for the region and resource group that the cluster is created in has the correct permissions. You can check who set the API key for the cluster by running `ibmcloud oc api-key info -c <cluster_name_or_ID>`.
    * If the account owner set the API key, then your cluster is assigned a {{site.data.keyword.cloudcerts_short}} instance.
    * If another user or a functional user set the API key, first [assign the user](/docs/openshift?topic=openshift-users#add_users) the **Administrator** or **Editor** platform access role and the **Manager** service access role for {{site.data.keyword.cloudcerts_short}} in **All resource groups**. Then, the user must [reset the API key for the region and resource group](/docs/openshift?topic=openshift-access-creds#api_key_most_cases). After the cluster has access to the updated permissions in the API key, your cluster is automatically assigned a {{site.data.keyword.cloudcerts_short}} instance.

The IBM-generated certificate for the default Ingress subdomain that exists in your cluster's {{site.data.keyword.cloudcerts_short}} instance. However, you have full control over your cluster's {{site.data.keyword.cloudcerts_short}} instance and can use {{site.data.keyword.cloudcerts_short}} to upload your own TLS certificates or order TLS certificates for your custom domains.

To view your {{site.data.keyword.cloudcerts_short}} instance:
1. Go to your [{{site.data.keyword.cloud_notm}} resource list](https://cloud.ibm.com/resources){: external}.
2. Expand the **Services** row.
3. Look for a {{site.data.keyword.cloudcerts_short}} instance that is named in the format `kube-certmgr-<cluster_ID>`. To find your cluster's ID, run `ibmcloud oc cluster ls`.
4. Click the instance's name. The **Your certificates** details page opens.

To manage the secrets for TLS certificates in your cluster, you can use the `ibmcloud oc ingress secret` set of commands. For example, you can use the `ibmcloud oc ingress secret create` command to import a certificate from {{site.data.keyword.cloudcerts_short}} to a Kubernetes secret in your cluster, or the `ibmcloud oc ingress secret ls -c <cluster>` command to view all Ingress secrets for TLS certificates in your cluster.

Do not delete your cluster's {{site.data.keyword.cloudcerts_short}} instance. When you delete your cluster, the {{site.data.keyword.cloudcerts_short}} instance for your cluster is also automatically deleted. Any certificates that are stored in the {{site.data.keyword.cloudcerts_short}} instance for your cluster are deleted when the {{site.data.keyword.cloudcerts_short}} instance is deleted.
{: important}

### Using the default TLS certificate for the IBM-provided Ingress subdomain
{: #manage_certs_ibm}

If you define the IBM-provided Ingress subdomain in your Ingress resource, you can also define the default TLS certificate for the Ingress subdomain.
{: shortdesc}

IBM-provided TLS certificates are signed by LetsEncrypt and are fully managed by IBM. The certificates expire every 90 days and are automatically renewed 37 days before they expire. To see the default certificate in your cluster's {{site.data.keyword.cloudcerts_long_notm}} instance, [click on the name of your cluster's {{site.data.keyword.cloudcerts_long_notm}} instance](https://cloud.ibm.com/resources){: external} to open the **Your certificates** page.

The TLS certificate is stored as an `Ingress secret` in the `openshift-ingress` project.

To get the secret name:
```sh
ibmcloud oc cluster get -c <cluster> | grep Ingress
```
{: pre}

To see the secret details:
```sh
ibmcloud oc ingress secret get -c <cluster> --name <secret_name> --namespace openshift-ingress
```
{: pre}

The Ingress controller can access TLS secrets only in the same project that the Ingress resource is deployed to. If your Ingress resources are deployed in projects other than `openshift-ingress`, you must copy the default TLS secret to those projects by running `ibmcloud oc ingress secret create --cluster <cluster_name_or_ID> --cert-crn <CRN> --name <secret_name> --namespace project`.
{: note}

The IBM-provided Ingress subdomain wildcard, `*.<cluster_name>.<globally_unique_account_HASH>-0000.<region>.containers.appdomain.cloud`, is registered by default for your cluster. The IBM-provided TLS certificate is a wildcard certificate and can be used for the wildcard subdomain.
{: tip}

### Using a TLS certificate for a custom subdomain
{: #manage_certs_custom}

If you define a custom subdomain in your Ingress resource, you can use your own TLS certificate to manage TLS termination.
{: shortdesc}

By storing custom TLS certificates in {{site.data.keyword.cloudcerts_long_notm}}, you can import the certificates directly into a Kubernetes secret in your cluster. To set up and manage TLS certificates for your custom Ingress subdomain in {{site.data.keyword.cloudcerts_short}}:

1. Open your {{site.data.keyword.cloudcerts_short}} instance in the [{{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/resources){: external}.
    You can store TLS certificates for your cluster in any {{site.data.keyword.cloudcerts_short}} instance your account, not just in the automatically-generated {{site.data.keyword.cloudcerts_short}} instance for your cluster.
    {: tip}

2. [Import](/docs/certificate-manager?topic=certificate-manager-managing-certificates-from-the-dashboard#importing-a-certificate) or [order](/docs/certificate-manager?topic=certificate-manager-ordering-certificates) a secret for your custom domain to {{site.data.keyword.cloudcerts_short}}. Keep in mind the following certificate considerations:
    * TLS certificates that contain pre-shared keys (TLS-PSK) are not supported.
    * If your custom domain is registered as a wildcard domain such as `*.custom_domain.net`, you must get a wildcard TLS certificate.

3. Import the certificate's associated secret into the same project where your Ingress resource for an app exists. If you want to use this certificate for apps in multiple projects, repeat this command for each project.
    Do not create the secret with the same name as the IBM-provided Ingress secret, which you can find by running `ibmcloud oc cluster get --cluster <cluster_name_or_ID> | grep Ingress`.
    {: note}

    ```sh
    ibmcloud oc ingress secret create --name <secret_name> --cluster <cluster_name_or_ID> --cert-crn <certificate_crn> --namespace <project>
    ```
    {: pre}

4. View the secret details. Secrets that you create from certificates in any instance are listed. The certificate's description is appended with the cluster ID and the secret name is in the format `k8s:cluster:<cluster-ID>:secret:<ALB-certificate-secret-name>`.
    ```sh
    ibmcloud oc ingress secret ls --cluster <cluster_name_or_ID>
    ```
    {: pre}

5. Optional: If you need to update your certificate, any changes that you make to a certificate in the {{site.data.keyword.cloudcerts_short}} instance that was created for your cluster are automatically reflected in the secret in your cluster. However, any changes that you make to a certificate in a different {{site.data.keyword.cloudcerts_short}} instance are not automatically reflected, and you must update the secret in your cluster the pick up the certificate changes.
    ```sh
    ibmcloud oc ingress secret update --name <secret_name> --cluster <cluster_name_or_ID> --namespace <project> [--cert-crn <certificate_crn>]
    ```
    {: pre}

## Migrating from {{site.data.keyword.cloudcerts_short}} to {{site.data.keyword.secrets-manager_short}}
{: #migrate-secrets-mgr}

With the deprecation of {{site.data.keyword.cloudcerts_long}}, you can now manage certificates with {{site.data.keyword.secrets-manager_short}}. For a comparison between the two services and details on migrating your resources, see [Migrating certificates from Certificate Manager](/docs/secrets-manager?topic=secrets-manager-migrate-from-certificate-manager#migrate-process). For migration instructions, see [Migration guidelines](/docs/secrets-manager?topic=secrets-manager-migrate-from-certificate-manager#migrate-guidelines).
{: shortdesc}

Support for the {{site.data.keyword.cloudcerts_short}} in Kubernetes clusters is set to end in late 2022, and any remaining {{site.data.keyword.cloudcerts_short}} instances are set to be deleted on 31 Dec 2022. Secrets in deleted {{site.data.keyword.cloudcerts_short}} are written directly to the cluster. If you do not migrate your secrets and set a default {{site.data.keyword.secrets-manager_short}}, your secrets are only written to the cluster and not to any manager instance.
{: note}

To learn how you can use {{site.data.keyword.secrets-manager_short}} with your {{site.data.keyword.redhat_openshift_notm}} cluster, see [Managing TLS and Opaque certificates and secrets with Secrets Manager](#manage_certs_secrets_mgr).

When migrating from {{site.data.keyword.cloudcerts_short}} to {{site.data.keyword.secrets-manager_short}}, keep the following points in mind:

**Secrets created in different namespaces**:
:   If you used your default {{site.data.keyword.cloudcerts_short}} instance to create secrets with Ingress CRNs in other namespaces, those CRNs become invalid once you register a {{site.data.keyword.secrets-manager_short}} default instance. Once you have set a {{site.data.keyword.secrets-manager_short}} instance as default, you must manually change those CRNs to match the new {{site.data.keyword.secrets-manager_short}} CRNs.

**Callback functionality to update secrets**:
:   Previously, {{site.data.keyword.cloudcerts_short}} provided a callback functionality to automatically update any Ingress secret created with a specific CRN if that secret CRN is updated in the default manager instance. This functionality is **not** available in {{site.data.keyword.secrets-manager_short}}. If you update a secret, you must run the `ibmcloud oc ingress secret update` command to apply the update to a Ingress secret with the CRN in the cluster. Otherwise, IBM Cloud periodically polls secrets for updates apply to the cluster, which may take up to 24 hours.

**Service-to-service enablement**:
:    If you want to enable service-to-service communication, you must [set up IAM credentials for {{site.data.keyword.secrets-manager_short}}](/docs/secrets-manager?topic=secrets-manager-configure-iam-engine&interface=ui) and [create a service-to-service authorization](/docs/secrets-manager?topic=secrets-manager-integrations#create-authorization).

**Migrating certificates stored with custom domains**:
:    For certificates stored with custom domains, you must manually upload the certificate to your secrets manager instance and update the secret with the corresponding new certificate CRN.

**Removing the registered Certificate Manager instance**:
:    Once you have successfully migrated to Secrets Manager, you can unregister the Certificate Manager instance that was provisioned with your cluster by running `ibmcloud oc ingress instance unregister`.

### Removing the {{site.data.keyword.cloudcerts_short}} instance from the cluster
{: #unregister-secret-instance}

After migrating to {{site.data.keyword.secrets-manager_short}}, a user can opt to remove the {{site.data.keyword.cloudcerts_short}} instance that is provisioned with the lifecycle of the cluster. Once this instance is removed, the callback functionality provided by {{site.data.keyword.cloudcerts_short}} is no longer available for the cluster.

Before you begin, verify that you have completed the following {{site.data.keyword.secrets-manager_short}} migration and setup steps.

1. [Registered a default {{site.data.keyword.secrets-manager_short}} instance](#default-secrets-mgr).
2. [Regenerated all nlb-dns subdomains and updated all non-IBM managed secrets with the new CRNs](#default-secrets-mgr).
3. Listed all secrets in the cluster and verified that no CRNs have `:cloudcert` in the CRN. If there are any, migrate and update as needed.
    ```sh
    ibmcloud oc ingress secret ls --cluster <cluster_name_or_id>
    ```
    {: pre}
    
4. [Enabled service-to-service between your cluster and {{site.data.keyword.secrets-manager_short}}](/docs/secrets-manager?topic=secrets-manager-integrations#create-authorization).

To remove the instance:

1. List the {{site.data.keyword.cloudcerts_short}} instances registered to the cluster. The instance name begins with `kube-certmgr-` or `kube-` and is of type `cloudcerts`.

    ```sh
    ibmcloud oc ingress instance ls --cluster <cluster_name_or_id>
    ```
    {: pre}

2. Unregister the {{site.data.keyword.cloudcerts_short}} instance from the cluster.

    ```sh
    ibmcloud oc ingress instance unregister --cluster <cluster_name_or_id> --name <instance_name>
    ```
    {: pre}

3. **Optional**: Delete the instance in the IBM Cloud Dashboard. If you do not delete the instance, it is automatically deleted when the {{site.data.keyword.cloudcerts_short}} service is deprecated.

## Managing TLS and Opaque certificates and secrets with {{site.data.keyword.secrets-manager_full}}
{: #manage_certs_secrets_mgr}

As of 11 April 2022, you can integrate your own {{site.data.keyword.secrets-manager_full_notm}} instances with your {{site.data.keyword.redhat_openshift_notm}} clusters. You can use {{site.data.keyword.secrets-manager_short}} instances across multiple clusters, and a single cluster can have more than one instance. For each cluster, you set one instance as a default where all Ingress subdomain certificates are uploaded. With the [`ibmcloud oc ingress secret` commands](/docs/containers?topic=containers-kubernetes-service-cli#cs_ingress_secret_create), you can also utilize {{site.data.keyword.secrets-manager_short}} to easily create and manage TLS or Opaque secrets that are stored in your {{site.data.keyword.redhat_openshift_notm}} cluster.
{: shortdesc}

**What secret types are supported with {{site.data.keyword.secrets-manager_short}}?**
:    {{site.data.keyword.secrets-manager_short}} supports IAM credentials, key-value secrets, user credentials, arbitrary secrets, and Kubernetes secrets. For more information on supported secrets, see [Working with secrets of different types](/docs/secrets-manager?topic=secrets-manager-what-is-secret#secret-types).
:    For Kubernetes secrets, {{site.data.keyword.secrets-manager_short}} supports both TLS and Opaque secret types. For TLS secrets, you can specify one certificate CRN. For Opaque secrets, you can specify multiple fields to pull non-certificate secrets. If you do not specify a secret type, TLS is applied by default.  

**Is a {{site.data.keyword.secrets-manager_short}} instance automatically generated in my cluster?**
:    No. You must [create a {{site.data.keyword.secrets-manager_short}} instance](/docs/secrets-manager?topic=secrets-manager-create-instance&interface=ui) and then [register your instance to your cluster](#register-secrets-mgr).

### Registering a {{site.data.keyword.secrets-manager_short}} instance to a cluster
{: #register-secrets-mgr}

After you have created a {{site.data.keyword.secrets-manager_short}} instance, you must register the instance to a cluster. After you have registered the instance to a cluster, an update to secret values in the instance also updates any secrets with a corresponding CRN.

```sh
ibmcloud oc ingress instance register --cluster <cluster_name_or_id> --crn <instance_crn>
```
{: pre}

If you want to register an instance to a cluster and also [set it as the default instance](#default-secrets-mgr), include the `--is-default` option. Otherwise, you can set a default instance with the `ibmcloud oc ingress instance set` command.
{: tip}

### Setting a {{site.data.keyword.secrets-manager_short}} instance as the default instance
{: #default-secrets-mgr}

When you set a default {{site.data.keyword.secrets-manager_short}} instance, all new Ingress subdomain certificates are stored in that instance. If a previous default instance had already been set, it is removed as the default.
{: shortdesc}

When you set a new default {{site.data.keyword.secrets-manager_short}} instance, any existing secrets that are not managed by IBM Cloud must have their certificate CRN manually updated to match the CRN of the new default instance. To update the CRN, use the `ibmcloud oc ingress secret update` command. If you do not update the CRN, these user-managed secrets do not update at the next scheduled certificate renewal.
{: important}

1. Run the command to set the new default.

    ```sh
    ibmcloud oc ingress instance default set --cluster <cluster_name_or_id> --crn <instance_crn> --name <instance_name>
    ```
    {: pre}

2. Regenerate your secrets. Any secrets that are managed by IBM are uploaded to the new default instance. 

    ```sh
    ibmcloud oc nlb-dns secret regenerate --cluster <cluster_name_or_id> --nlb-subdomain <nlb_subdomain>
    ```
    {: pre}

3. If the subdomain you specified in the `ibmcloud oc nlb-dns secret regenerate` command also corresponds to any secret that is not managed by IBM, you must manually update the CRN of that secret.

    To check whether or not a secret is managed by IBM Cloud, run `ibmcloud oc ingress secret get` to view the details of the secret. In the output, if **User Managed** is marked **false**, the secret is managed by IBM Cloud. If it is marked **true**, the secret is not managed by IBM Cloud.
    {: tip}

    1. List the secrets in the cluster and note the CRN of the updated secrets that correspond with the subdomain. 

        ```sh
        ibmcloud oc ingress secret ls --cluster <cluster_name_or_id>
        ```
        {: pre}

        Example output.

        ```sh
        Name                                                             Namespace        CRN                                                                                                                                                              Expires On                 Domain                                                                                                  Status    Type   
        pvg-classic-111aaaaa1aaa-1a1111aa11a111a1aaa1aaa111111a11-000   default          crn:v1:staging:public:cloudcerts:us-south:a/1a11a1a111aa11aa111aa1a1111aa1a1:a111a1aa-1aa1-111-aa11-a1a1a111aa1a:certificate:1aaa1aaa1a111a1a1111a11a111a11a1    2022-08-01T08:49:42+0000   pvg-classic-111aaaaa1aaa-1a1111aa11a111a1aaa1aaa111111a11-000.us-east.stg.containers.appdomain.cloud   created   TLS   
        pvg-classic-111aaaaa1aaa-1a1111aa11a111a1aaa1aaa111111a11-000   ibm-cert-store   crn:v1:staging:public:cloudcerts:us-south:a/1a11a1a111aa11aa111aa1a1111aa1a1:a111a1aa-1aa1-111-aa11-a1a1a111aa1a:certificate:1aaa1aaa1a111a1a1111a11a111a11a1   2022-08-01T08:49:42+0000   pvg-classic-111aaaaa1aaa-1a1111aa11a111a1aaa1aaa111111a11-000.us-east.stg.containers.appdomain.cloud   created   TLS   
        pvg-classic-111aaaaa1aaa-1a1111aa11a111a1aaa1aaa111111a11-000   kube-system      crn:v1:staging:public:cloudcerts:us-south:a/1a11a1a111aa11aa111aa1a1111aa1a1:a111a1aa-1aa1-111-aa11-a1a1a111aa1a:certificate:1aaa1aaa1a111a1a1111a11a111a11a1   2022-08-01T08:49:42+0000   pvg-classic-111aaaaa1aaa-1a1111aa11a111a1aaa1aaa111111a11-000.us-east.stg.containers.appdomain.cloud   created   TLS  

        ```
        {: screen}

    2. Update the non-IBM managed secrets with the CRN of the matching subdomain you found earlier. 

        ```sh
        ibmcloud oc ingress secret update --cluster <cluster_name_or_id> --name <secret_name> --namespace <namespace> --cert-crn <updated_crn>
        ```
        {: pre}
    

#### Removing a {{site.data.keyword.secrets-manager_short}} instance as the default instance
{: #secret-mgr-remove-default}

To remove a {{site.data.keyword.secrets-manager_short}} instance as the default instance of a cluster, run the following command. Note that if no default instance is set, your secrets are only written directly to the cluster and are not uploaded to any {{site.data.keyword.secrets-manager_short}} instance.

```sh
ibmcloud oc ingress instance default unset --cluster <cluster_name_or_id> --crn <instance_crn> --name <instance_name>
```
{: pre}


## Customizing Ingress routing with annotations
{: #annotations-roks4}

If you want to customize routing rules for your app, you can use [route-specific HAProxy annotations](https://docs.openshift.com/container-platform/4.9/networking/routes/route-configuration.html#nw-route-specific-annotations_route-configuration){: external} in the Ingress resources that you define.

These supported annotations are in the format `haproxy.router.openshift.io/<annotation>` or `router.openshift.io/<annotation>`.{{site.data.keyword.containerlong_notm}} annotations (`ingress.bluemix.net/<annotation>`) and NGINX annotations (`nginx.ingress.kubernetes.io/<annotation>`) are not supported for the Ingress controller or the Ingress resource in {{site.data.keyword.redhat_openshift_notm}} version 4.
{: important}

