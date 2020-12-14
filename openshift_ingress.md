---

copyright:
  years: 2014, 2020
lastupdated: "2020-12-14"

keywords: openshift, roks, rhoks, rhos, nginx, ingress controller

subcollection: openshift

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:api: .ph data-hd-interface='api'}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
{:codeblock: .codeblock}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:fuzzybunny: .ph data-hd-programlang='fuzzybunny'}
{:generic: data-hd-operatingsystem="generic"}
{:generic: data-hd-programlang="generic"}
{:gif: data-image-type='gif'}
{:go: .ph data-hd-programlang='go'}
{:help: data-hd-content-type='help'}
{:hide-dashboard: .hide-dashboard}
{:hide-in-docs: .hide-in-docs}
{:important: .important}
{:ios: data-hd-operatingsystem="ios"}
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:new_window: target="_blank"}
{:note .note}
{:note: .note}
{:objectc data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:route: data-hd-keyref="route"}
{:row-headers: .row-headers}
{:ruby: .ph data-hd-programlang='ruby'}
{:ruby: data-hd-programlang="ruby"}
{:runtime: architecture="runtime"}
{:runtimeIcon: .runtimeIcon}
{:runtimeIconList: .runtimeIconList}
{:runtimeLink: .runtimeLink}
{:runtimeTitle: .runtimeTitle}
{:screen: .screen}
{:script: data-hd-video='script'}
{:service: architecture="service"}
{:service_instance_name: data-hd-keyref="service_instance_name"}
{:service_name: data-hd-keyref="service_name"}
{:shortdesc: .shortdesc}
{:space_name: data-hd-keyref="space_name"}
{:step: data-tutorial-type='step'}
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:tutorial: data-hd-content-type='tutorial'}
{:ui: .ph data-hd-interface='ui'}
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vbnet: .ph data-hd-programlang='vb.net'}
{:video: .video}



# Setting up {{site.data.keyword.openshiftlong_notm}} Ingress in {{site.data.keyword.openshiftshort}} 3.11
{: #ingress}

Expose multiple apps in your {{site.data.keyword.openshiftshort}} cluster by creating Ingress resources that are managed by the IBM-provided application load balancer in {{site.data.keyword.openshiftlong}}.
{: shortdesc}

<img src="images/icon-version-311.png" alt="Version 3.11 icon" width="30" style="width:30px; border-style: none"/> This information is for clusters that run {{site.data.keyword.openshiftshort}} version 3.11 only. To set up Ingress for {{site.data.keyword.openshiftshort}} version 4, see [Setting up Ingress in {{site.data.keyword.openshiftshort}} version 4](/docs/openshift?topic=openshift-ingress-roks4).
{: important}

## Quick start
{: #ingress-qs}
{: help}
{: support}

Quickly expose your app to the Internet by creating an Ingress resource.
{: shortdesc}

First time setting up Ingress? Check out the other sections on this page for prerequisite, planning, and detailed setup steps. Come back to these quick start steps for a brief refresher the next time you set up an Ingress resource.
{: tip}



This quick start is for clusters that run {{site.data.keyword.openshiftshort}} version 3.11 only. For clusters that run {{site.data.keyword.openshiftshort}} version 4, see [Quick start for Ingress in {{site.data.keyword.openshiftshort}} version 4](/docs/openshift?topic=openshift-ingress-qs-roks4).
{: important}

1. Create a Kubernetes ClusterIP service for your app so that it can be included in the Ingress application load balancing.
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

3. Using the Ingress subdomain and secret, create an Ingress resource file. Replace `<app_path>` with the path that your app listens on. If your app does not listen on a specific path, define the root path as a slash (<code>/</code>) only.
  ```yaml
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


## Prerequisites
{: #config_prereqs}

Before you get started with Ingress, review the following prerequisites.
{: shortdesc}

- Enable a [Virtual Router Function (VRF)](/docs/account?topic=account-vrf-service-endpoint#vrf) for your IBM Cloud infrastructure account. To enable VRF, [contact your IBM Cloud infrastructure account representative](/docs/account?topic=account-vrf-service-endpoint#vrf). To check whether a VRF is already enabled, use the `ibmcloud account show` command. If you cannot or do not want to enable VRF, enable [VLAN spanning](/docs/vlans?topic=vlans-vlan-spanning#vlan-spanning). When a VRF or VLAN spanning is enabled, the ALB can route packets to various subnets in the account.
- Setting up Ingress requires the following [{{site.data.keyword.cloud_notm}} IAM roles](/docs/openshift?topic=openshift-users#platform):
    - **Administrator** platform role for the cluster
    - **Manager** service role in all namespaces
- Ingress is available for standard clusters only and requires at least two worker nodes per zone to ensure high availability and that periodic updates are applied. If you have only one worker in a zone, the ALB cannot receive automatic updates. When automatic updates are rolled out to ALB pods, the pod is reloaded. However, ALB pods have anti-affinity rules to ensure that only one pod is scheduled to each worker node for high availability. Because there is only one ALB pod on one worker, the pod is not restarted so that traffic is not interrupted. The ALB pod is updated to the latest version only when you delete the old pod manually so that the new, updated pod can be scheduled.
- If you restrict network traffic to edge worker nodes, ensure that at least two [edge worker nodes](/docs/openshift?topic=openshift-edge) are enabled in each zone so that ALBs deploy uniformly.
- To be included in Ingress load balancing, the names of the `ClusterIP` services that expose your apps must be unique across all namespaces in your cluster.
- If a zone fails, you might see intermittent failures in requests to the Ingress ALB in that zone.

<br />

## Planning networking for single or multiple namespaces
{: #multiple_namespaces}

One Ingress resource is required per namespace where you have apps that you want to expose.
{: shortdesc}

### All apps are in one namespace
{: #one-ns}

If the apps in your cluster are all in the same namespace, one Ingress resource is required to define routing rules for the apps that are exposed there.
{: shortdesc}

For example, if you have `app1` and `app2` exposed by services in a development namespace, you can create an Ingress resource in the namespace. The resource specifies `domain.net` as the host and registers the paths that each app listens on with `domain.net`.

<img src="images/cs_ingress_single_ns.png" width="270" alt="One resource is required per namespace." style="width:270px; border-style: none"/>

### Apps are in multiple namespaces
{: #multi-ns}

If the apps in your cluster are in different namespaces, you must create one resource per namespace to define rules for the apps that are exposed there.
{: shortdesc}

However, you can define a hostname in only one resource. You cannot define the same hostname in multiple resources. To register multiple Ingress resources with the same hostname, you must use a wildcard domain. When a wildcard domain such as `*.domain.net` is registered, multiple subdomains can all resolve to the same host. Then, you can create an Ingress resource in each namespace and specify a different subdomain in each Ingress resource.

For example, consider the following scenario:
* You have two versions of the same app, `app1` and `app3`, for testing purposes.
* You deploy the apps in two different namespaces within the same cluster: `app1` into the development namespace, and `app3` into the staging namespace.

To use the same cluster ALB to manage traffic to these apps, you create the following services and resources:
* A Kubernetes service in the development namespace to expose `app1`.
* An Ingress resource in the development namespace that specifies the host as `dev.domain.net`.
* A Kubernetes service in the staging namespace to expose `app3`.
* An Ingress resource in the staging namespace that specifies the host as `stage.domain.net`.
</br>
<img src="images/cs_ingress_multi_ns.png" width="625" alt="Within a namespace, use subdomains in one or multiple resources" style="width:625px; border-style: none"/>

Now, both URLs resolve to the same domain and are thus both serviced by the same ALB. However, because the resource in the staging namespace is registered with the `stage` subdomain, the Ingress ALB correctly routes requests from the `stage.domain.net/app3` URL to only `app3`.

{: #wildcard_tls}
The IBM-provided Ingress subdomain wildcard, `*.<cluster_name>.<globally_unique_account_HASH>-0000.<region>.containers.appdomain.cloud`, is registered by default for your cluster. The IBM-provided TLS certificate is a wildcard certificate and can be used for the wildcard subdomain. If you want to use a wildcard custom domain, you must register the custom domain as a wildcard domain such as `*.custom_domain.net`, and to use TLS, you must get a wildcard certificate.
{: note}

### Multiple domains within a namespace
{: #multi-domains}

Within an individual namespace, you can use one domain to access all the apps in the namespace. If you want to use different domains for the apps within an individual namespace, use a wildcard domain. When a wildcard domain such as `*.mycluster-<hash>-0000.us-south.containers.appdomain.cloud` is registered, multiple subdomains all resolve to the same host. Then, you can use one resource to specify multiple subdomain hosts within that resource. Alternatively, you can create multiple Ingress resources in the namespace and specify a different subdomain in each Ingress resource.
{: shortdesc}

<img src="images/cs_ingress_single_ns_multi_subs.png" width="625" alt="One resource is required per namespace." style="width:625px; border-style: none"/>

The IBM-provided Ingress subdomain wildcard, `*.<cluster_name>.<globally_unique_account_HASH>-0000.<region>.containers.appdomain.cloud`, is registered by default for your cluster. The IBM-provided TLS certificate is a wildcard certificate and can be used for the wildcard subdomain. If you want to use a wildcard custom domain, you must register the custom domain as a wildcard domain such as `*.custom_domain.net`, and to use TLS, you must get a wildcard certificate.
{: note}

<br />

## Exposing apps that are inside your cluster to the public
{: #ingress_expose_public}

Expose apps that are inside your cluster to the public by using the public Ingress ALB.
{: shortdesc}

**Before you begin:**

* Review the Ingress [prerequisites](#config_prereqs).
* [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

### Step 1: Deploy apps and create app services
{: #public_inside_1}

Start by deploying your apps and creating Kubernetes services to expose them.
{: shortdesc}

1.  [Deploy your app to the cluster](/docs/openshift?topic=openshift-openshift_apps). Ensure that you add a label to your deployment in the metadata section of your configuration file, such as `app: code`. This label is needed to identify all pods where your app runs so that the pods can be included in the Ingress load balancing.
2.   For each app deployment that you want to expose, create a Kubernetes `ClusterIP` service. Your app must be exposed by a Kubernetes service to be included in the Ingress load balancing.
      ```
      oc expose deploy <app_deployment_name> --name my-app-svc --port <app_port> -n <namespace>
      ```
      {: pre}

### Step 2: Select an app domain
{: #public_inside_2}

When you configure the public ALB, you choose the domain that your apps will be accessible through.
{: shortdesc}

**IBM-provided Ingress domain:** You can use the IBM-provided domain, such as `mycluster-<hash>-0000.us-south.containers.appdomain.cloud/myapp`, to access your app from the internet.

Get the IBM-provided domain. To get the cluster name or ID where your app is deployed, run `ibmcloud oc cluster ls`.
```
ibmcloud oc cluster get --cluster <cluster_name_or_ID> | grep Ingress
```
{: pre}

Example output:
```
Ingress Subdomain:      mycluster-<hash>-0000.us-south.containers.appdomain.cloud
Ingress Secret:         mycluster-<hash>-0000
```
{: screen}

**Custom domain:** To use a custom domain instead, you can set up a CNAME record to map your custom domain to the IBM-provided domain.
1.    Create a custom domain. To register your custom domain, work with your Domain Name Service (DNS) provider or [{{site.data.keyword.cloud_notm}} DNS](/docs/dns?topic=dns-getting-started). If you want to use different subdomains for your apps, register the custom domain as a wildcard domain, such as `*.custom_domain.net`. Note that domains are limited to 255 characters or fewer.
2.  Define an alias for your custom domain by specifying the IBM-provided domain as a Canonical Name record (CNAME). To find the IBM-provided Ingress domain, run `ibmcloud oc cluster get --cluster <cluster_name>` and look for the **Ingress subdomain** field.

### Step 3: Select TLS termination
{: #public_inside_3}

After you choose the app domain, you choose whether to use TLS termination.
{: shortdesc}

The ALB load balances HTTP network traffic to the apps in your cluster. To also load balance incoming HTTPS connections, you can configure the ALB to decrypt the network traffic and forward the decrypted request to the apps that are exposed in your cluster.

For more information about TLS certificates, see [Managing TLS certificates and secrets](#manage_certs).

**If you use the IBM-provided Ingress domain:** Use the IBM-provided TLS certificate, which is stored as a Kubernetes secret in the `default` namespace.

Get the IBM-provided TLS secret for your cluster.
```
ibmcloud oc cluster get --cluster <cluster_name_or_ID> | grep Ingress
```
{: pre}

Example output:
```
Ingress Subdomain:      mycluster-<hash>-0000.us-south.containers.appdomain.cloud
Ingress Secret:         mycluster-<hash>-0000
```
{: screen}
</br>

**If you use a custom domain:** Use your own TLS certificate to manage TLS termination. If a TLS certificate is stored in {{site.data.keyword.cloudcerts_long_notm}} that you want to use, you can import its associated secret into your cluster by running the following command:

```
ibmcloud oc ingress secret create --name <secret_name> --cluster <cluster_name_or_ID> --cert-crn <certificate_crn> [--namespace <project>]
```
{: pre}

If you do not specify a project, the certificate secret is created in a project called `ibm-cert-store`. A reference to this secret is then created in the `default` project, which any Ingress resource in any project can access. When the ALB is processing requests, it follows this reference to pick up and use the certificate secret from the `ibm-cert-store` project. Note that TLS certificates that contain pre-shared keys (TLS-PSK) are not supported.

Do not create the secret with the same name as the IBM-provided Ingress secret, which you can find by running `ibmcloud oc cluster get --cluster <cluster_name_or_ID> | grep Ingress`.
{: note}

</br>

If you do not have a TLS certificate ready, follow these steps:
1. Generate a certificate authority (CA) cert and key from your certificate provider. If you have your own domain, purchase an official TLS certificate for your domain. Make sure the [CN](https://support.dnsimple.com/articles/what-is-common-name/){: external} is different for each certificate.
2. Convert the cert and key into base64.
   1. Encode the cert and key into base64 and save the base64 encoded value in a new file.
      ```
      openssl base64 -in tls.key -out tls.key.base64
      ```
      {: pre}

   2. View the base64 encoded value for your cert and key.
      ```
      cat tls.key.base64
      ```
      {: pre}

3. Create a secret YAML file using the cert and key.
     ```yaml
     apiVersion: v1
     kind: Secret
     metadata:
       name: ssl-my-test
     type: Opaque
     data:
       tls.crt: <client_certificate>
       tls.key: <client_key>
     ```
     {: codeblock}

4. Create a Kubernetes secret for your certificate.
     ```
     oc apply -f ssl-my-test
     ```
     {: pre}
     Do not create the secret with the same name as the IBM-provided Ingress secret, which you can find by running `ibmcloud oc cluster get --cluster <cluster_name_or_ID> | grep Ingress`.
     {: note}


### Step 4: Create the Ingress resource
{: #public_inside_4}

Ingress resources define the routing rules that the ALB uses to route traffic to your app service.
{: shortdesc}

If your cluster has multiple namespaces where apps are exposed, one Ingress resource is required per namespace. However, each namespace must use a different host. You must register a wildcard domain and specify a different subdomain in each resource. For more information, see [Planning networking for single or multiple namespaces](#multiple_namespaces).
{: note}

1. Open your preferred editor and create an Ingress configuration file that is named, for example, `myingressresource.yaml`.

2. Define an Ingress resource in your configuration file that uses the IBM-provided domain or your custom domain to route incoming network traffic to the services that you created earlier.

    Example YAML that does not use TLS:
    ```yaml
    apiVersion: extensions/v1beta1
    kind: Ingress
    metadata:
      name: myingressresource
    spec:
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

    Example YAML that uses TLS:
    ```yaml
    apiVersion: extensions/v1beta1
    kind: Ingress
    metadata:
      name: myingressresource
    spec:
      tls:
      - hosts:
        - <domain>
        secretName: <tls_secret_name>
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

    <table summary="The columns are read from left to right. The first column has the parameter of the YAML file. The second column describes the parameter.">
    <caption>Ingress resource YAML file components</caption>
    <col width="20%">
    <thead>
    <th>Parameter</th>
    <th>Description</th>
    </thead>
    <tbody>
    <tr>
    <td><code>tls.hosts</code></td>
    <td>To use TLS, replace <em>&lt;domain&gt;</em> with the IBM-provided Ingress subdomain or your custom domain.</br></br><strong>Note:</strong><ul><li>If your apps are exposed by services in different namespaces in one cluster, add a wildcard subdomain to the beginning of the domain, such as `subdomain1.custom_domain.net` or `subdomain1.mycluster-<hash>-0000.us-south.containers.appdomain.cloud`. Use a unique subdomain for each resource that you create in the cluster.</li><li>Do not use &ast; for your host or leave the host property empty to avoid failures during Ingress creation.</li></ul></td>
    </tr>
    <tr>
    <td><code>tls.secretName</code></td>
    <td><ul><li>If you use the IBM-provided Ingress domain, replace <em>&lt;tls_secret_name&gt;</em> with the name of the IBM-provided Ingress secret.</li><li>If you use a custom domain, replace <em>&lt;tls_secret_name&gt;</em> with the secret that you created earlier that holds your custom TLS certificate and key. If you imported a certificate from {{site.data.keyword.cloudcerts_short}}, you can run <code>ibmcloud oc ingress secret ls --cluster <cluster_name_or_ID></code> to see the secrets in your cluster.</li><ul><td>
    </tr>
    <tr>
    <td><code>host</code></td>
    <td>Replace <em>&lt;domain&gt;</em> with the IBM-provided Ingress subdomain or your custom domain.
    </br></br>
    <strong>Note:</strong><ul><li>If your apps are exposed by services in different namespaces in one cluster, add a wildcard subdomain to the beginning of the domain, such as `subdomain1.custom_domain.net` or `subdomain1.mycluster-<hash>-0000.us-south.containers.appdomain.cloud`. Use a unique subdomain for each resource that you create in the cluster.</li><li>Do not use &ast; for your host or leave the host property empty to avoid failures during Ingress creation.</li></ul></td>
    </tr>
    <tr>
    <td><code>path</code></td>
    <td>Replace <em>&lt;app_path&gt;</em> with a slash or the path that your app is listening on. The path is appended to the IBM-provided or your custom domain to create a unique route to your app. When you enter this route into a web browser, network traffic is routed to the ALB. The ALB looks up the associated service and sends network traffic to the service. The service then forwards the traffic to the pods where the app runs.
    </br></br>
    Many apps do not listen on a specific path, but use the root path and a specific port. In this case, define the root path as <code>/</code> and do not specify an individual path for your app. Examples: <ul><li>For <code>http://domain/</code>, enter <code>/</code> as the path.</li><li>For <code>http://domain/app1_path</code>, enter <code>/app1_path</code> as the path.</li></ul>
    <p class="tip">To configure Ingress to listen on a path that is different than the path that your app listens on, you can use the [rewrite annotation](/docs/openshift?topic=openshift-ingress_annotation#rewrite-path).</p></td>
    </tr>
    <tr>
    <td><code>serviceName</code></td>
    <td>Replace <em>&lt;app1_service&gt;</em> and <em>&lt;app2_service&gt;</em>, and so on, with the name of the services you created to expose your apps. If your apps are exposed by services in different namespaces in the cluster, include only app services that are in the same namespace. You must create one Ingress resource for each namespace where you have apps that you want to expose.</td>
    </tr>
    <tr>
    <td><code>servicePort</code></td>
    <td>The port that your service listens to. Use the same port that you defined when you created the Kubernetes service for your app.</td>
    </tr>
    </tbody></table>

3.  Create the Ingress resource for your cluster. Ensure that the resource deploys into the same namespace as the app services that you specified in the resource.
    ```
    oc apply -f myingressresource.yaml -n <namespace>
    ```
    {: pre}
4.   Verify that the Ingress resource was created successfully. If messages in the events describe an error in your resource configuration, change the values in your resource file and reapply the file for the resource.

    ```
    oc describe ingress myingressresource
    ```
    {: pre}

Your Ingress resource is created in the same namespace as your app services. Your apps in this namespace are registered with the cluster's Ingress ALB.

### Step 5: Access your app from the internet
{: #public_inside_5}

In a web browser, enter the URL of the app service to access.
{: shortdesc}

```
https://<domain>/<app1_path>
```
{: codeblock}

If you exposed multiple apps, access those apps by changing the path that is appended to the URL.

```
https://<domain>/<app2_path>
```
{: codeblock}

If you use a wildcard domain, access those apps with their own subdomains.

```
http://<subdomain1>.<domain>/<app1_path>
```
{: codeblock}

```
http://<subdomain2>.<domain>/<app1_path>
```
{: codeblock}

<p class="tip">Having trouble connecting to your app through Ingress? Try [Troubleshooting Ingress](/docs/openshift?topic=openshift-cs_troubleshoot_debug_ingress). You can check the health and status of your Ingress components by running `ibmcloud oc ingress status -c <cluster_name_or_ID>`.</p>

<br />

## Exposing apps that are outside your cluster to the public
{: #external_endpoint}

Expose apps that are outside your cluster to the public by including them in public Ingress ALB load balancing. Incoming public requests on the IBM-provided or your custom domain are forwarded automatically to the external app.
{: shortdesc}

You have two options for setting up routing to an external app:
* To forward requests directly to the IP address of your external service, [set up a Kubernetes endpoint](#external_ip) that defines the external IP address and port of the app.
* To route requests through the Ingress ALB to your external service, [use the `proxy-external-service` annotation](#proxy-external) in your Ingress resource file.

### Exposing external apps through a Kubernetes endpoint
{: #external_ip}

Forward requests directly to the IP address of your external service by setting up a Kubernetes endpoint that defines the external IP address and port of the app.
{: shortdesc}

**Before you begin:**
* Review the Ingress [prerequisites](#config_prereqs).
* Ensure that the external app that you want to include into the cluster load balancing can be accessed by using a public IP address.
* [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

To expose apps that are outside of your cluster to the public:
1.  Define a Kubernetes service configuration file for the app that the ALB will expose. This service forwards incoming requests to an external endpoint that you create in subsequent steps.
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

2.  Create the service in your cluster.
    ```
    oc apply -f myexternalservice.yaml
    ```
    {: pre}

3.  Define an external endpoint configuration file. Include all public IP addresses and ports that you can use to access your external app. Note that the name of the endpoint must be the same as the name of the service that you defined in the previous step, `myexternalservice`.

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

    <table summary="The columns are read from left to right. The first column has the parameter of the YAML file. The second column describes the parameter.">
    <caption>Ingress resource YAML file components</caption>
    <col width="20%">
    <thead>
    <th>Parameter</th>
    <th>Description</th>
    </thead>
    <tbody>
    <tr>
    <td><code>name</code></td>
    <td>Replace <em><code>&lt;myexternalendpoint&gt;</code></em> with the name of the Kubernetes service that you created earlier.</td>
    </tr>
    <tr>
    <td><code>ip</code></td>
    <td>Replace <em>&lt;external_IP&gt;</em> with the public IP addresses to connect to your external app.</td>
     </tr>
     <td><code>port</code></td>
     <td>Replace <em>&lt;external_port&gt;</em> with the port that your external app listens to.</td>
     </tbody></table>

4.  Create the endpoint in your cluster.
    ```
    oc apply -f myexternalendpoint.yaml
    ```
    {: pre}

5. Continue with the steps in "Exposing apps that are inside your cluster to the public", [Step 2: Select an app domain](#public_inside_2).

### Exposing external apps through the `proxy-external-service` Ingress annotation
{: #proxy-external}

Route requests through the Ingress ALB to your external service by using the `proxy-external-service` annotation in your Ingress resource file.
{: shortdesc}

**Before you begin:**
* Review the Ingress [prerequisites](#config_prereqs).
* [Access your {{site.data.keyword.openshiftshort}} cluster](/docs/openshift?topic=openshift-access_cluster).

To expose apps that are outside of your cluster to the public:

1. [Choose the app domain](#public_inside_2) that you want the external service to be accessible from.

2. Create an Ingress resource file that is named, for example, `myingressresource.yaml`.
  ```yaml
  apiVersion: extensions/v1beta1
  kind: Ingress
  metadata:
    name: myingress
    annotations:
      ingress.bluemix.net/proxy-external-service: "path=<mypath> external-svc=https:<external_service> host=<ingress_subdomain>"
  spec:
    rules:
    - host: <ingress_subdomain>
  ```
  {: codeblock}

  <table summary="The columns are read from left to right. The first column has the parameter of the YAML file. The second column describes the parameter.">
  <caption>Ingress resource YAML file components</caption>
  <col width="20%">
  <thead>
  <th>Parameter</th>
  <th>Description</th>
  </thead>
  <tbody>
  <tr>
  <td><code>path</code></td>
  <td>Replace <code>&lt;<em>mypath</em>&gt;</code> with the path that the external service listens on.</td>
  </tr>
  <tr>
  <td><code>external-svc</code></td>
  <td>Replace <code>&lt;<em>external_service</em>&gt;</code> with the external service to be called. For example, <code>https://&lt;myservice&gt;.&lt;region&gt;.appdomain.com</code>.</td>
  </tr>
  <tr>
  <td><code>host</code></td>
  <td>Replace <code>&lt;<em>ingress_subdomain</em>&gt;</code> with the Ingress subdomain for your cluster or the custom domain that you set up.</td>
  </tr>
  </tbody></table>

  <p class="tip">If you also want to define other services that are _inside_ your cluster, you can follow the steps in [Exposing apps that are inside your cluster to the public](#ingress_expose_public) to add them to this Ingress resource file.</p>

3.  Create the Ingress resource for your cluster.

    ```
    oc apply -f myingressresource.yaml
    ```
    {: pre}
4.   Verify that the Ingress resource was created successfully. If messages in the events describe an error in your resource configuration, change the values in your resource file and reapply the file for the resource.

    ```
    oc describe ingress myingressresource
    ```
    {: pre}
5. In a web browser, enter the URL of the app service to access.
  ```
  https://<domain>/<app_path>
  ```
  {: codeblock}

<p class="tip">Having trouble connecting to your app through Ingress? Try [Troubleshooting Ingress](/docs/openshift?topic=openshift-cs_troubleshoot_debug_ingress). You can check the health and status of your Ingress components by running `ibmcloud oc ingress status -c <cluster_name_or_ID>`.</p>

<br />

## Exposing apps to a private network
{: #ingress_expose_private}

<img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Expose apps to a private network by using the private Ingress ALBs.
{: shortdesc}

To use a private ALB, you must first enable the private ALB. Because private VLAN-only clusters are not assigned an IBM-provided Ingress subdomain, no Ingress secret is created during cluster setup. To expose your apps to the private network, you must register your ALB with a custom domain and, optionally, import your own TLS certificate.

**Before you begin:**
* Review the Ingress [prerequisites](#config_prereqs).

### Step 1: Deploy apps and create app services
{: #private_1}

Start by deploying your apps and creating Kubernetes services to expose them.
{: shortdesc}

1.  [Deploy your app to the cluster](/docs/openshift?topic=openshift-openshift_apps). Ensure that you add a label to your deployment in the metadata section of your configuration file, such as `app: code`. This label is needed to identify all pods where your app runs so that the pods can be included in the Ingress load balancing.
2.   For each app deployment that you want to expose, create a Kubernetes `ClusterIP` service. Your app must be exposed by a Kubernetes service to be included in the Ingress load balancing.
      ```
      oc expose deploy <app_deployment_name> --name my-app-svc --port <app_port> -n <namespace>
      ```
      {: pre}

</br>

### Step 2: Enable the default private ALB
{: #private_ingress}

When you create a standard cluster, a private ALB is created in each zone that you have worker nodes and assigned a private IP address. However, the default private ALB in each zone is not automatically enabled. You must first enable each private ALB.
{: shortdesc}

1. Get the private ALB IDs for your cluster.
    ```
    ibmcloud oc ingress alb ls --cluster <cluster_name>
    ```
    {: pre}

    The field **Status** for private ALBs is _disabled_.
    ```
    ALB ID                                            Enabled   Status     Type      ALB IP          Zone    Build                          ALB VLAN ID   NLB Version
    private-crdf253b6025d64944ab99ed63bb4567b6-alb1   false     disabled   private   -               dal10   ingress:2410/ingress-auth:947   2234947       -
    public-crdf253b6025d64944ab99ed63bb4567b6-alb1    true      enabled    public    169.xx.xxx.xxx  dal10   ingress:2410/ingress-auth:947   2234945       -
    ```
    {: screen}

2. Get the default version of the {{site.data.keyword.openshiftlong_notm}} Ingress image.
  ```
  ibmcloud oc ingress alb versions
  ```
  {: pre}

  In the following example output, the default {{site.data.keyword.openshiftlong_notm}} Ingress version is `2410`:
  ```
  IBM Cloud Ingress: 'auth' version
  947

  IBM Cloud Ingress versions
  2410 (default)
  662
  658

  Kubernetes Ingress versions
  0.35.0_767_iks (default)
  0.34.1_764_iks
  0.33.0_768_iks
  ```
  {: screen}

3. Enable the private ALBs. Run this command for the ID of each private ALB that you want to enable. If you want to specify an IP address for the ALB, include the IP address in the `--ip` flag.
  ```
  ibmcloud oc ingress alb enable classic --alb <private_ALB_ID> -c <cluster_name_or_ID> --version 2410
  ```
  {: pre}
  </br>

### Step 3: Map your custom domain
{: #private_3}

When you configure the private ALBs, you must expose your apps by using a custom domain.
{: shortdesc}

1.    Create a custom domain. To register your custom domain, work with your Domain Name Service (DNS) provider or [{{site.data.keyword.cloud_notm}} DNS](/docs/dns?topic=dns-getting-started). If you want to use different subdomains for your apps, register the custom domain as a wildcard domain, such as `*.custom_domain.net`. Note that domains are limited to 255 characters or fewer.
2.  Map your custom domain to the portable private IP addresses of the ALBs by adding the IP addresses as A records. To find the portable private IP addresses of the ALBs, run `ibmcloud oc ingress alb get --alb  <private_alb_ID>` for each ALB.
</br>

### Step 4: Select TLS termination
{: #private_4}

After you map your custom domain, choose whether to use TLS termination.
{: shortdesc}

To load balance incoming HTTPS connections, you can configure the ALB to decrypt the network traffic and forward the decrypted request to the apps that are exposed in your cluster. You can use your own TLS certificate to manage TLS termination for your custom domain.

If a TLS certificate is stored in {{site.data.keyword.cloudcerts_long_notm}} that you want to use, you can import its associated secret into your cluster by running the following command:

```
ibmcloud oc ingress secret create --name <secret_name> --cluster <cluster_name_or_ID> --cert-crn <certificate_crn> [--namespace <project>]
```
{: pre}

If you do not specify a project, the certificate secret is created in a project called `ibm-cert-store`. A reference to this secret is then created in the `default` project, which any Ingress resource in any project can access. When the ALB is processing requests, it follows this reference to pick up and use the certificate secret from the `ibm-cert-store` project. Note that TLS certificates that contain pre-shared keys (TLS-PSK) are not supported.

For more information about TLS certificates, see [Managing TLS certificates and secrets](#manage_certs).

</br>

### Step 5: Create the Ingress resource
{: #private_5}

Ingress resources define the routing rules that the ALB uses to route traffic to your app service.
{: shortdesc}

If your cluster has multiple namespaces where apps are exposed, one Ingress resource is required per namespace. However, each namespace must use a different host. You must register a wildcard domain and specify a different subdomain in each resource. For more information, see [Planning networking for single or multiple namespaces](#multiple_namespaces).
{: note}

1. Open your preferred editor and create an Ingress configuration file that is named, for example, `myingressresource.yaml`.

2.  Define an Ingress resource in your configuration file that uses your custom domain to route incoming network traffic to the services that you created earlier.

    Example YAML that does not use TLS:
    ```yaml
    apiVersion: extensions/v1beta1
    kind: Ingress
    metadata:
      name: myingressresource
      annotations:
        ingress.bluemix.net/ALB-ID: "<private_ALB_ID_1>;<private_ALB_ID_2>"
    spec:
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

    Example YAML that uses TLS:
    ```yaml
    apiVersion: extensions/v1beta1
    kind: Ingress
    metadata:
      name: myingressresource
      annotations:
        ingress.bluemix.net/ALB-ID: "<private_ALB_ID_1>;<private_ALB_ID_2>"
    spec:
      tls:
      - hosts:
        - <domain>
        secretName: <tls_secret_name>
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

    <table summary="The columns are read from left to right. The first column has the parameter of the YAML file. The second column describes the parameter.">
    <caption>Ingress resource YAML file components</caption>
    <col width="25%">
    <thead>
    <th>Parameter</th>
    <th>Description</th>
    </thead>
    <tbody>
    <tr>
    <td><code>ingress.bluemix.net/ALB-ID</code></td>
    <td>Replace <em>&lt;private_ALB_ID&gt;</em> with the ID for your private ALB. If you have a multizone cluster and enabled multiple private ALBs, include the ID of each ALB. Run <code>ibmcloud oc ingress alb ls --cluster &lt;my_cluster&gt;</code> to find the ALB IDs. For more information about this Ingress annotation, see [Private application load balancer routing](/docs/openshift?topic=openshift-ingress_annotation#alb-id).</td>
    </tr>
    <tr>
    <td><code>tls.hosts</code></td>
    <td>To use TLS, replace <em>&lt;domain&gt;</em> with your custom domain.</br></br><strong>Note:</strong><ul><li>If your apps are exposed by services in different namespaces in one cluster, add a wildcard subdomain to the beginning of the domain, such as `subdomain1.custom_domain.net`. Use a unique subdomain for each resource that you create in the cluster.</li><li>Do not use &ast; for your host or leave the host property empty to avoid failures during Ingress creation.</li></ul></td>
    </tr>
    <tr>
    <td><code>tls.secretName</code></td>
    <td>Replace <em>&lt;tls_secret_name&gt;</em> with the name of the secret that you created earlier and that holds your custom TLS certificate and key. If you imported a certificate from {{site.data.keyword.cloudcerts_short}}, you can run <code>ibmcloud oc ingress secret ls --cluster <cluster_name_or_ID></code> to see the secrets in your cluster.
    </tr>
    <tr>
    <td><code>host</code></td>
    <td>Replace <em>&lt;domain&gt;</em> with your custom domain.
    </br></br>
    <strong>Note:</strong><ul><li>If your apps are exposed by services in different namespaces in one cluster, add a wildcard subdomain to the beginning of the domain, such as `subdomain1.custom_domain.net`. Use a unique subdomain for each resource that you create in the cluster.</li><li>Do not use &ast; for your host or leave the host property empty to avoid failures during Ingress creation.</li></ul></td>
    </td>
    </tr>
    <tr>
    <td><code>path</code></td>
    <td>Replace <em>&lt;app_path&gt;</em> with a slash or the path that your app is listening on. The path is appended to your custom domain to create a unique route to your app. When you enter this route into a web browser, network traffic is routed to the ALB. The ALB looks up the associated service and sends network traffic to the service. The service then forwards the traffic to the pods where the app runs.
    </br></br>
    Many apps do not listen on a specific path, but use the root path and a specific port. In this case, define the root path as <code>/</code> and do not specify an individual path for your app. Examples: <ul><li>For <code>http://domain/</code>, enter <code>/</code> as the path.</li><li>For <code>http://domain/app1_path</code>, enter <code>/app1_path</code> as the path.</li></ul>
    <p class="tip">To configure Ingress to listen on a path that is different than the path that your app listens on, you can use the [rewrite annotation](/docs/openshift?topic=openshift-ingress_annotation#rewrite-path).</p>
    </tr>
    <tr>
    <td><code>serviceName</code></td>
    <td>Replace <em>&lt;app1_service&gt;</em> and <em>&lt;app2_service&gt;</em>, and so on, with the name of the services you created to expose your apps. If your apps are exposed by services in different namespaces in the cluster, include only app services that are in the same namespace. You must create one Ingress resource for each namespace where you have apps that you want to expose.</td>
    </tr>
    <tr>
    <td><code>servicePort</code></td>
    <td>The port that your service listens to. Use the same port that you defined when you created the Kubernetes service for your app.</td>
    </tr>
    </tbody></table>

3.  Create the Ingress resource for your cluster. Ensure that the resource deploys into the same namespace as the app services that you specified in the resource.
    ```
    oc apply -f myingressresource.yaml -n <namespace>
    ```
    {: pre}
4.   Verify that the Ingress resource was created successfully. If messages in the events describe an error in your resource configuration, change the values in your resource file and reapply the file for the resource.

    ```
    oc describe ingress myingressresource
    ```
    {: pre}

Your Ingress resource is created in the same namespace as your app services. Your apps in this namespace are registered with the cluster's Ingress ALB.
</br>

### Step 6: Access your app from your private network
{: #private_6}

1. Before you can access your app, make sure that you can access a DNS service.
  * Public and private VLAN: To use the default external DNS provider, you must [configure edge nodes with public access](/docs/openshift?topic=openshift-edge#edge) and [configure a Virtual Router Appliance](https://www.ibm.com/blogs/cloud-archive/2017/07/kubernetes-and-bluemix-container-based-workloads-part4/){: external}.
  * Private VLAN only: You must configure a [DNS service that is available on the private network](https://kubernetes.io/docs/tasks/administer-cluster/dns-custom-nameservers/){: external}.

2. From within your private network firewall, enter the URL of the app service in a web browser.

```
https://<domain>/<app1_path>
```
{: codeblock}

If you exposed multiple apps, access those apps by changing the path that is appended to the URL.

```
https://<domain>/<app2_path>
```
{: codeblock}

If you use a wildcard domain, access those apps with their own subdomains.

```
http://<subdomain1>.<domain>/<app1_path>
```
{: codeblock}

```
http://<subdomain2>.<domain>/<app1_path>
```
{: codeblock}

<p class="tip">Having trouble connecting to your app through Ingress? Try [Troubleshooting Ingress](/docs/openshift?topic=openshift-cs_troubleshoot_debug_ingress). You can check the health and status of your Ingress components by running `ibmcloud oc ingress status -c <cluster_name_or_ID>`.</p>

### Optional: Block traffic to public NodePorts
{: #block-nodeports}

In clusters that are connected to public and private VLANs, block traffic to public NodePorts.
{: shortdesc}

Ingress ALBs make your app available over both the ALB IP address and port, and the service's NodePorts. NodePorts are accessible on every IP address (public and private) for every node within the cluster. If your cluster is attached to both public and private VLANs, an ALB with a portable private IP address still has a public NodePort open on every worker node. Create a [Calico preDNAT network policy](/docs/openshift?topic=openshift-network_policies#block_ingress) to block traffic to the public NodePorts.

<br />

## Managing TLS certificates and secrets
{: #manage_certs}

Create and manage the TLS certificates and secrets for your Ingress subdomains.
{: pre}

To load balance incoming HTTPS connections to your subdomain, you can configure the ALB to decrypt the network traffic and forward the decrypted request to the apps that are exposed in your cluster.

### Using TLS certificates in {{site.data.keyword.cloudcerts_short}}
{: #manage_certs_about}

As of 24 August 2020, an [{{site.data.keyword.cloudcerts_long}}](/docs/certificate-manager?topic=certificate-manager-about-certificate-manager) instance is automatically created for each cluster that you can use to manage the cluster's Ingress TLS certificates.
{: shortdesc}

For a {{site.data.keyword.cloudcerts_short}} instance to be created for your new or existing cluster, ensure that the API key for the region and resource group that the cluster is created in has the correct permissions.
  * If the account owner, who already has the required permissions, set the API key, then your cluster is assigned a {{site.data.keyword.cloudcerts_short}} instance.
  * If another user or a functional user set the API key, first [assign the user](/docs/openshift?topic=openshift-users#add_users) the **Administrator** or **Editor** platform role and the **Manager** service role for {{site.data.keyword.cloudcerts_short}} in **All resource groups**. Then, the user must [reset the API key for the region and resource group](/docs/openshift?topic=openshift-users#api_key_most_cases). After the cluster has access the updated permissions in the API key, your cluster is automatically assigned a {{site.data.keyword.cloudcerts_short}} instance.

To view your {{site.data.keyword.cloudcerts_short}} instance:
1. In the {{site.data.keyword.cloud_notm}} console, navigate to your [{{site.data.keyword.cloud_notm}} resource list](https://cloud.ibm.com/resources){: external}.
2. Expand the **Services** row.
3. Look for a {{site.data.keyword.cloudcerts_short}} instance that is named in the format `kube-<cluster_ID>`. To find your cluster's ID, run `ibmcloud oc cluster ls`.
4. Click the instance's name. The **Your certificates** details page opens.

The IBM-generated certificate for the default Ingress subdomain exists in your cluster's {{site.data.keyword.cloudcerts_short}} instance. However, you have full control over your cluster's {{site.data.keyword.cloudcerts_short}} instance and can use {{site.data.keyword.cloudcerts_short}} to upload your own TLS certificates or order TLS certificates for your custom domains.

To manage the secrets for TLS certificates in your cluster, you can use the `ibmcloud oc ingress secret` set of commands.
* For example, you can import a certificate from {{site.data.keyword.cloudcerts_short}} to a Kubernetes secret in your cluster:
  ```
  ibmcloud oc ingress secret create --cluster <cluster_name_or_ID> --cert-crn <crn> --name <secret_name> --namespace project
  ```
  {: pre}
* To view all Ingress secrets for TLS certificates in your cluster:
  ```
  ibmcloud oc ingress secret ls -c <cluster>
  ```
  {: pre}

Do not delete your cluster's {{site.data.keyword.cloudcerts_short}} instance. When you delete your cluster, the {{site.data.keyword.cloudcerts_short}} instance for your cluster is also automatically deleted. Any certificates that are stored in the {{site.data.keyword.cloudcerts_short}} instance for your cluster are deleted when the {{site.data.keyword.cloudcerts_short}} instance is deleted.
{: important}

### Using the default TLS certificate for the IBM-provided Ingress subdomain
{: #manage_certs_ibm}

If you define the IBM-provided Ingress subdomain in your Ingress resource, you can also define the default TLS certificate for the Ingress subdomain.
{: shortdesc}

IBM-provided TLS certificates are signed by LetsEncrypt and are fully managed by IBM. The certificates expire every 90 days and are automatically renewed 37 days before they expire. To see the default certificate in your cluster's {{site.data.keyword.cloudcerts_long_notm}} instance, [click on the name of your cluster's {{site.data.keyword.cloudcerts_long_notm}} instance](https://cloud.ibm.com/resources){: external} to open the **Your certificates** page.

The TLS certificate is stored as a Kubernetes secret in the `default` project.

To get the secret name:
```
ibmcloud oc cluster get -c <cluster> | grep Ingress
```
{: pre}

To see the secret details:
```
ibmcloud oc ingress secret get -c <cluster> --name <secret_name> --namespace default
```
{: pre}

The IBM-provided Ingress subdomain wildcard, `*.<cluster_name>.<globally_unique_account_HASH>-0000.<region>.containers.appdomain.cloud`, is registered by default for your cluster. The IBM-provided TLS certificate is a wildcard certificate and can be used for the wildcard subdomain.
{: tip}

### Using a TLS certificate for a custom subdomain
{: #manage_certs_custom}

If you define a custom subdomain in your Ingress resource, you can use your own TLS certificate to manage TLS termination.
{: shortdesc}

By storing custom TLS certificates in {{site.data.keyword.cloudcerts_long_notm}}, you can import the certificates directly into a Kubernetes secret in your cluster. To set up and manage TLS certificates for your custom Ingress subdomain in {{site.data.keyword.cloudcerts_short}}:

1. Open your {{site.data.keyword.cloudcerts_short}} instance in the [{{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/resources){: external}.<p class="tip">You can store TLS certificates for your cluster in any {{site.data.keyword.cloudcerts_short}} instance your account, not just in the automatically-generated {{site.data.keyword.cloudcerts_short}} instance for your cluster.</p>

2. [Import](/docs/certificate-manager?topic=certificate-manager-managing-certificates-from-the-dashboard#importing-a-certificate) or [order](/docs/certificate-manager?topic=certificate-manager-ordering-certificates) a secret for your custom domain to {{site.data.keyword.cloudcerts_short}}. Keep in mind the following certificate considerations:
  * TLS certificates that contain pre-shared keys (TLS-PSK) are not supported.
  * If your custom domain is registered as a wildcard domain such as `*.custom_domain.net`, you must get a wildcard TLS certificate.

3. Import the certificate's associated secret into your cluster. If you have apps in one project only, you can specify that project in the `--namespace` flag. If you have apps in multiple projects, do not specify the `--namespace` flag so that the secret is created in the `ibm-cert-store` project. A reference to this secret is then created in the `default` project, which any Ingress resource in any project can access. When the ALB is processing requests, it follows this reference to pick up and use the certificate secret from the `ibm-cert-store` project.<p class="note">Do not create the secret with the same name as the IBM-provided Ingress secret, which you can find by running `ibmcloud oc cluster get --cluster <cluster_name_or_ID> | grep Ingress`.</p>
  ```
  ibmcloud oc ingress secret create --name <secret_name> --cluster <cluster_name_or_ID> --cert-crn <certificate_crn> [--namespace <project>]
  ```
  {: pre}

4. View the secret details. Secrets that you create from certificates in any instance are listed. The certificate's description is appended with the cluster ID and the secret name is in the format `k8s:cluster:<cluster-ID>:secret:<ALB-certificate-secret-name>`.
  ```
  ibmcloud oc ingress secret ls --cluster <cluster_name_or_ID>
  ```
  {: pre}

5. Optional: If you need to update your certificate, any changes that you make to a certificate in the {{site.data.keyword.cloudcerts_short}} instance that was created for your cluster are automatically reflected in the secret in your cluster. However, any changes that you make to a certificate in a different {{site.data.keyword.cloudcerts_short}} instance are not automatically reflected, and you must update the secret in your cluster the pick up the certificate changes.
  ```
  ibmcloud oc ingress secret update --name <secret_name> --cluster <cluster_name_or_ID> --namespace <project> [--cert-crn <certificate_crn>]
  ```
  {: pre}

<br />



## Opening non-default ports in the Ingress ALB
{: #opening_ingress_ports}

Expose non-default ports for the Ingress ALB.
{: shortdesc}

1. Edit the YAML file for the `ibm-cloud-provider-ingress-cm` configmap.
  ```
  oc edit cm ibm-cloud-provider-ingress-cm -n kube-system
  ```
  {: pre}

2. Add a `data` section and specify the public ports `80`, `443`, and any other ports you want to expose separated by a semi-colon (;).

    By default, ports 80 and 443 are open. If you want to keep 80 and 443 open, you must also include them in addition to any other ports you specify in the `public-ports` field. Any port that is not specified is closed. If you enabled a private ALB, you must also specify any ports that you want to keep open in the `private-ports` field.
    {: important}

    Example that keeps ports `80`, `443`, and `9443` open:
    ```yaml
    apiVersion: v1
    data:
      public-ports: "80;443;9443"
    kind: ConfigMap
    metadata:
      name: ibm-cloud-provider-ingress-cm
      namespace: kube-system
    ```
    {: screen}

3. Save the configuration file.

4. Verify that the configmap changes were applied. The changes are applied to your ALBs automatically.
  ```
  oc get cm ibm-cloud-provider-ingress-cm -n kube-system -o yaml
  ```
  {: pre}

5. Optional:
  * Access an app via a non-standard TCP port that you opened by using the [`tcp-ports`](/docs/openshift?topic=openshift-ingress_annotation#tcp-ports) annotation.
  * Change the default ports for HTTP (port 80) and HTTPS (port 443) network traffic to a port that you opened by using the [`custom-port`](/docs/openshift?topic=openshift-ingress_annotation#custom-port) annotation.

<br />

## Updating ALBs
{: #alb-update}

Choose the image type and image version for your ALBs, and keep the image version for your ALB pods up to date.
{: shortdesc}

### Choosing a supported image version
{: #alb-version-choose}

You can manage the versions of your ALBs in the following ways:
* When you create a new ALB, enable an ALB that was previously disabled, or manually update an ALB, you can specify an image version for your ALB in the `--version` flag.
* To specify a version other than the default, you must first disable automatic updates by running the `ibmcloud oc ingress alb autoupdate disable` command.
* If you omit the `--version` flag when you enable or update an existing ALB, the ALB runs the default version of the {{site.data.keyword.openshiftlong_notm}} Ingress image.

To list the latest three versions that are supported for each type of image, run the following command:
```
ibmcloud oc ingress alb versions
```
{: pre}

Example output:
```
IBM Cloud Ingress: 'auth' version
947

IBM Cloud Ingress versions
2410 (default)
662
658

Kubernetes Ingress versions
0.35.0_767_iks (default)
0.34.1_764_iks
0.33.0_768_iks
```
{: screen}Note that only the custom {{site.data.keyword.cloud_notm}} Ingress image versions are supported for {{site.data.keyword.openshiftshort}} clusters. For the changes that are included in each version of the {{site.data.keyword.cloud_notm}} Ingress image, see the [Ingress version changelog](/docs/containers?topic=containers-cluster-add-ons-changelog#alb_changelog).

### Managing automatic updates
{: #autoupdate}

Manage automatic updates of all Ingress ALB pods in a cluster.
{: shortdesc}

By default, automatic updates to Ingress ALBs are enabled. ALB pods are automatically updated by IBM when a new image version is available.

You can disable or enable the automatic updates for all Ingress ALBs in your cluster.
* To disable automatic updates:
  ```
  ibmcloud oc ingress alb autoupdate disable -c <cluster_name_or_ID>
  ```
  {: pre}
* To re-enable automatic updates:
  ```
  ibmcloud oc ingress alb autoupdate enable -c <cluster_name_or_ID>
  ```
  {: pre}

If automatic updates for the Ingress ALB add-on are disabled and you want to update the add-on, you can force a one-time update of your ALB pods.After you force a one-time update, automatic updates remain disabled.
* To update all ALB pods in the cluster:
  ```
  ibmcloud oc ingress alb update -c <cluster_name_or_ID> --version <image_version>
  ```
  {: pre}
* To update the ALB pods for one or more specific ALBs:
  ```
  ibmcloud oc ingress alb update -c <cluster_name_or_ID> --version <image_version> --alb <ALB_ID> [--alb <ALB_2_ID> ...]
  ```
  {: pre}

### Reverting to an earlier version
{: #revert}

If your ALB pods were recently updated, but a custom configuration for your ALBs is affected by the latest image version build, you can use the `ibmcloud oc ingress alb update --version <image_version>` command to roll back ALB pods to an earlier, supported version.
{: shortdesc}

The image version that you change your ALB to must be a supported image version that is listed in the output of `ibmcloud oc ingress alb versions`. After you force a one-time update, automatic updates to your ALBs are disabled.

<br />

## Scaling ALBs
{: #scale_albs}

When you create a standard cluster, one public and one private ALB is created in each zone where you have worker nodes. Each ALB can handle 32,768 connections per second. However, if you must process more than 32,768 connections per second, you can scale up your ALBs by increasing the number of ALB pod replicas or by creating more ALBs.
{: shortdesc}

### Increasing the number of ALB pod replicas
{: #alb_replicas}

By default, each ALB has 2 replicas. Scale up your ALB processing capabilities by increasing the number of ALB pods.
{: shortdesc}

1. Get the IDs for your ALBs.
  ```
  ibmcloud oc ingress alb ls -c <cluster_name_or_ID>
  ```
  {: pre}

2. Create a YAML file for an `ibm-ingress-deploy-config` configmap. For each ALB, add `'{"replicas":<number_of_replicas>}'`. Example for increasing the number of ALB pods to 4 replicas:
   ```yaml
   apiVersion: v1
   kind: ConfigMap
   metadata:
     name: ibm-ingress-deploy-config
     namespace: kube-system
   data:
     <alb1-id>: '{"replicas":<number_of_replicas>}'
     <alb2-id>: '{"replicas":<number_of_replicas>}'
     ...
   ```
   {: screen}

3. Create the `ibm-ingress-deploy-config` configmap in your cluster.
  ```
  oc create -f ibm-ingress-deploy-config.yaml
  ```
  {: pre}

4. To pick up the changes, update your ALBs.
  ```
  ibmcloud oc ingress alb update -c <cluster_name_or_ID>
  ```
  {: pre}

5. Verify that the number of ALB pods that are `Ready` are increased to the number of replicas that you specified.
  ```
  oc get pods -n kube-system | grep alb
  ```
  {: pre}

### Creating more ALBs
{: #create_alb}

Scale up your ALB processing capabilities by creating more ALBs.
{: shortdesc}

For example, if you have worker nodes in `dal10`, a default public ALB exists in `dal10`. This default public ALB is deployed as two pods on two worker nodes in that zone. However, to handle more connections per second, you want to increase the number of ALBs in `dal10`. You can create a second public ALB in `dal10`. This ALB is also deployed as two pods on two worker nodes in `dal10`. All public ALBs in your cluster share the same IBM-assigned Ingress subdomain, so the IP address of the new ALB is automatically added to your Ingress subdomain. You do not need to change your Ingress resource files.

You can also use these steps to create more ALBs across zones in your cluster. When you create a multizone cluster, a default public ALB is created in each zone where you have worker nodes. However, default public ALBs are created in only up to three zones. If, for example, you later remove one of these original three zones and add workers in a different zone, a default public ALB is not created in that new zone. You can manually create an ALB to process connections in that new zone.
{: tip}

1. In each zone where you have worker nodes, create an ALB. For more information about this command's parameters, see the [CLI reference](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_alb_create).
  ```
  ibmcloud oc ingress alb create --cluster <cluster_name_or_ID> --type <public_or_private> --zone <zone> --vlan <VLAN_ID> [--ip <IP_address>] [--version image_version]
  ```
  {: pre}

2. Verify that the ALBs that you created in each zone have a **Status** of `enabled` and that an **ALB IP** is assigned.
  ```
  ibmcloud oc ingress alb ls --cluster <cluster_name_or_ID>
  ```
  {: pre}

  Example output for a cluster in which new public ALBs with IDs of `public-crdf253b6025d64944ab99ed63bb4567b6-alb3` and `public-crdf253b6025d64944ab99ed63bb4567b6-alb4` are created in `dal10` and `dal12`:
  ```
  ALB ID                                            Enabled   Status     Type      ALB IP          Zone    Build                          ALB VLAN ID   NLB Version
  private-crdf253b6025d64944ab99ed63bb4567b6-alb1   false     disabled   private   -               dal12   ingress:2410/ingress-auth:947   2294021       -
  private-crdf253b6025d64944ab99ed63bb4567b6-alb2   false     disabled   private   -               dal10   ingress:2410/ingress-auth:947   2234947       -
  public-crdf253b6025d64944ab99ed63bb4567b6-alb1    true      enabled    public    169.48.228.78   dal12   ingress:2410/ingress-auth:947   2294019       -
  public-crdf253b6025d64944ab99ed63bb4567b6-alb2    true      enabled    public    169.46.17.6     dal10   ingress:2410/ingress-auth:947   2234945       -
  public-crdf253b6025d64944ab99ed63bb4567b6-alb3    true      enabled    public    169.49.28.09    dal12   ingress:2410/ingress-auth:947   2294019       -
  public-crdf253b6025d64944ab99ed63bb4567b6-alb4    true      enabled    public    169.50.35.62    dal10   ingress:2410/ingress-auth:947   2234945       -
  ```
  {: screen}

3. If you later decide to scale down your ALBs, you can disable an ALB. For example, you might want to disable an ALB to use less compute resources on your worker nodes. The ALB is disabled and does not route traffic in your cluster. You can re-enable an ALB at any time by running `ibmcloud oc ingress alb enable classic --alb <ALB_ID> -c <cluster_name_or_ID>`.
  ```
  ibmcloud oc ingress alb disable --alb <ALB_ID> -c <cluster_name_or_ID>
  ```
  {: pre}
  </br>

<br />

## Moving ALBs across VLANs
{: #migrate-alb-vlan}

<img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> The information in this topic is specific to classic clusters only.
{: note}

When you [change your worker node VLAN connections](/docs/openshift?topic=openshift-cs_network_cluster#change-vlans), the worker nodes are connected to the new VLAN and assigned new public or private IP addresses. However, ALBs cannot automatically migrate to the new VLAN because they are assigned a stable, portable public or private IP address from a subnet that belongs to the old VLAN. When your worker nodes and ALBs are connected to different VLANs, the ALBs cannot forward incoming network traffic to app pods to your worker nodes. To move your ALBs to a different VLAN, you must create an ALB on the new VLAN and disable the ALB on the old VLAN.
{: shortdesc}

Note that all public ALBs in your cluster share the same IBM-assigned Ingress subdomain. When you create new ALBs, you do not need to change your Ingress resource files.

1. Get the new public or private VLAN that you changed your worker node connections to in each zone.
  1. List the details for a worker in a zone.
    ```
    ibmcloud oc worker get --cluster <cluster_name_or_ID> --worker <worker_id>
    ```
    {: pre}

  2. In the output, note the **ID** for the public or the private VLAN.
    * To create public ALBs, note the public VLAN ID.
    * To create private ALBs, note the private VLAN ID.

  3. Repeat these steps for a worker in each zone so that you have the IDs for the new public or private VLAN in each zone.

2. In each zone, create an ALB on the new VLAN. For more information about this command's parameters, see the [CLI reference](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_alb_create).
  ```
  ibmcloud oc ingress alb create --cluster <cluster_name_or_ID> --type <public_or_private> --zone <zone> --vlan <VLAN_ID> [--ip <IP_address>] [--version image_version]
  ```
  {: pre}

3. Verify that the ALBs that you created on the new VLANs in each zone have a **Status** of `enabled` and that an **ALB IP** address is assigned.
    ```
    ibmcloud oc ingress alb ls --cluster <cluster_name_or_ID>
    ```
    {: pre}

    Example output for a cluster in which new public ALBs are created on VLAN `2294030` in `dal12` and `2234940` in `dal10`:
    ```
    ALB ID                                            Enabled   Status     Type      ALB IP          Zone    Build                          ALB VLAN ID   NLB Version
    private-crdf253b6025d64944ab99ed63bb4567b6-alb1   false     disabled   private   -               dal12   ingress:2410/ingress-auth:947   2294021
    private-crdf253b6025d64944ab99ed63bb4567b6-alb2   false     disabled   private   -               dal10   ingress:2410/ingress-auth:947   2234947
    public-crdf253b6025d64944ab99ed63bb4567b6-alb1    true      enabled    public    169.48.228.78   dal12   ingress:2410/ingress-auth:947   2294019
    public-crdf253b6025d64944ab99ed63bb4567b6-alb2    true      enabled    public    169.46.17.6     dal10   ingress:2410/ingress-auth:947   2234945
    public-crdf253b6025d64944ab99ed63bb4567b6-alb3    true      enabled    public    169.49.28.09    dal12   ingress:2410/ingress-auth:947   2294030
    public-crdf253b6025d64944ab99ed63bb4567b6-alb4    true      enabled    public    169.50.35.62    dal10   ingress:2410/ingress-auth:947   2234940
    ```
    {: screen}

4. Disable each ALB that is connected to the old VLANs.
  ```
  ibmcloud oc ingress alb disable --alb <old_ALB_ID> -c <cluster_name_or_ID>
  ```
  {: pre}

5. Verify that each ALB that is connected to the old VLANs has a **Status** of `disabled`. Only the ALBs that are connected to the new VLANs receive incoming network traffic and communicate with your app pods.
    ```
    ibmcloud oc ingress alb ls --cluster <cluster_name_or_ID>
    ```
    {: pre}

    Example output for a cluster in which the default public ALBs on VLAN `2294019` in `dal12` and `2234945` in `dal10`: are disabled:
    ```
    ALB ID                                            Enabled   Status     Type      ALB IP          Zone    Build
    private-crdf253b6025d64944ab99ed63bb4567b6-alb1   false     disabled   private   -               dal12   ingress:2410/ingress-auth:947   2294021
    private-crdf253b6025d64944ab99ed63bb4567b6-alb2   false     disabled   private   -               dal10   ingress:2410/ingress-auth:947   2234947
    public-crdf253b6025d64944ab99ed63bb4567b6-alb1    false     disabled   public    169.48.228.78   dal12   ingress:2410/ingress-auth:947   2294019
    public-crdf253b6025d64944ab99ed63bb4567b6-alb2    false     disabled   public    169.46.17.6     dal10   ingress:2410/ingress-auth:947   2234945
    public-crdf253b6025d64944ab99ed63bb4567b6-alb3    true      enabled    public    169.49.28.09    dal12   ingress:2410/ingress-auth:947   2294030
    public-crdf253b6025d64944ab99ed63bb4567b6-alb4    true      enabled    public    169.50.35.62    dal10   ingress:2410/ingress-auth:947   2234940
    ```
    {: screen}

6. Optional for public ALBs: Verify that the IP addresses of the new ALBs are listed under the IBM-provided Ingress subdomain for your cluster. You can find this subdomain by running `ibmcloud oc cluster get --cluster <cluster_name_or_ID>`.
  ```
  nslookup <Ingress_subdomain>
  ```
  {: pre}

  Example output:
  ```
  Non-authoritative answer:
  Name:    mycluster-<hash>-0000.us-south.containers.appdomain.cloud
  Addresses:  169.49.28.09
            169.50.35.62
  ```
  {: screen}

7. Optional: If you no longer need the subnets on the old VLANs, you can [remove them](/docs/openshift?topic=openshift-subnets#remove-subnets).

<br />

## Increasing the restart readiness check time for ALB pods
{: #readiness-check}

Increase the amount of time that ALB pods have to parse large Ingress resource files when the ALB pods restart.
{: shortdesc}

When an ALB pod restarts, such as after an update is applied, a readiness check prevents the ALB pod from attempting to route traffic requests until all of the Ingress resource files are parsed. This readiness check prevents request loss when ALB pods restart. By default, the readiness check waits 15 seconds after the pod restarts to start checking whether all Ingress files are parsed. If all files are parsed 15 seconds after the pod restarts, the ALB pod begins to route traffic requests again. If all files are not parsed 15 seconds after the pod restarts, the pod does not route traffic, and the readiness check continues to check every 15 seconds for a maximum timeout of 5 minutes. After 5 minutes, the ALB pod begins to route traffic.

If you have very large Ingress resource files, it might take longer than 5 minutes for all of the files to be parsed. You can change the default values for the readiness check interval rate and for the total maximum readiness check timeout by adding the `ingress-resource-creation-rate` and `ingress-resource-timeout` settings to the `ibm-cloud-provider-ingress-cm` configmap.

1. Edit the configuration file for the `ibm-cloud-provider-ingress-cm` configmap resource.
    ```
    oc edit cm ibm-cloud-provider-ingress-cm -n kube-system
    ```
    {: pre}

2. In the **data** section, add the `ingress-resource-creation-rate` and `ingress-resource-timeout` settings. Values can be formatted as seconds (`s`) and minutes (`m`). Example:
   ```yaml
   apiVersion: v1
   data:
     ingress-resource-creation-rate: 1m
     ingress-resource-timeout: 6m
     keep-alive: 8s
     private-ports: 80;443
     public-ports: 80;443
   ```
   {: codeblock}

3. Save the configuration file.

4. Verify that the configmap changes were applied. The changes are applied to your ALBs automatically.
   ```
   oc get cm ibm-cloud-provider-ingress-cm -n kube-system -o yaml
   ```
   {: pre}


