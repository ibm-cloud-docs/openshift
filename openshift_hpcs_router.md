---

copyright:
  years: 2014, 2022
lastupdated: "2022-07-01"

keywords: openshift, route, router

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}


# Encrypting routes with keys stored in {{site.data.keyword.hscrypto}}
{: #hpcs-router}

Deploy the {{site.data.keyword.cloud_notm}} HPCS Router to encrypt routes with a private key that is stored in an [{{site.data.keyword.cloud}} {{site.data.keyword.hscrypto}} instance](/docs/hs-crypto?topic=hs-crypto-get-started).
{: shortdesc}

{{site.data.keyword.cloud_notm}} HPCS Router add-on is deprecated and become unsupported on 15 August 2022.
{: important}

{{site.data.keyword.hscrypto}} allows you to securely create, store, and manage encryption keys in {{site.data.keyword.cloud_notm}}. A private key that is stored in an {{site.data.keyword.hscrypto}} instance can be used by an {{site.data.keyword.redhat_openshift_notm}} router in [TLS session establishment](/docs/hs-crypto?topic=hs-crypto-use-cases#ssl-offloading) and in Certificate Signing Request (CSR) signing. To access {{site.data.keyword.hscrypto}}, an {{site.data.keyword.redhat_openshift_notm}} router must use the [OpenSSL Engine](https://github.com/openssl/openssl/blob/OpenSSL_1_1_1-stable/README.ENGINE){: external} `grep11` to make calls to the [Enterprise PKCS #11 over gRPC (GREP11) API](/docs/hs-crypto?topic=hs-crypto-introduce-cloud-hsm#access-cloud-hsm-grep11). However, the default router in {{site.data.keyword.openshiftlong_notm}} version 4 clusters can't be configured to use an alternative OpenSSL Engine integration.

Instead, you can deploy the custom {{site.data.keyword.cloud_notm}} HPCS Router, which uses the `grep11` OpenSSL Engine to access private keys that are stored in an {{site.data.keyword.hscrypto}} instance to encrypt routes. The {{site.data.keyword.cloud_notm}} HPCS Router is managed by an {{site.data.keyword.redhat_openshift_notm}} operator, and provides the same route management system as the default router.

In the following steps, you:
1. Set up router sharding to ensure the default router does not process routes that are encrypted with a key from {{site.data.keyword.hscrypto}}.
2. Enable the {{site.data.keyword.cloud_notm}} HPCS Router operator in OperatorHub and install the operator in your cluster.
3. Use the operator to create a router, set {{site.data.keyword.hscrypto}} instance data as environment variables for the router, and choose a router domain.
4. Use the operator to generate and sign a CSR with a private key that is stored in {{site.data.keyword.hscrypto}}, and send the CSR to a certificate authority to get a certificate for your router domain.
5. Use the certificate to create an encrypted route that exposes your app.

## Before you begin
{: #hpcs-router-prereqs}

Before you begin, complete the following {{site.data.keyword.hscrypto}} and {{site.data.keyword.openshiftlong_notm}} tasks.
{: shortdesc}

1. [Provision an {{site.data.keyword.hscrypto}} instance](/docs/hs-crypto?topic=hs-crypto-get-started).
2. [Initialize the {{site.data.keyword.hscrypto}} instance](/docs/hs-crypto?topic=hs-crypto-initialize-hsm)
3. [Create a Key in your {{site.data.keyword.hscrypto}} instance](/docs/hs-crypto?topic=hs-crypto-create-root-keys).
4. Make sure that you have the {{site.data.keyword.cloud_notm}} IAM [**Administrator** platform access role](/docs/openshift?topic=openshift-users) for {{site.data.keyword.containershort_notm}} for the cluster and the [**Manager** service access role](/docs/openshift?topic=openshift-users) {{site.data.keyword.containershort_notm}} for the cluster in all namespaces (projects).
5. [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster). Note that the {{site.data.keyword.cloud_notm}} HPCS Router is supported only for {{site.data.keyword.redhat_openshift_notm}} version 4.5 and later.

## Step 1: Set up default router sharding
{: #sharding}

Before you deploy the HPCS router into your cluster, set up router sharding to ensure that only the HPCS router processes routes that are encrypted with a key that is stored in {{site.data.keyword.hscrypto}}.
{: shortdesc}

By default, any router that is created in your cluster is configured to process any routes that you create. By using [router sharding](https://docs.openshift.com/container-platform/4.9/networking/configuring_ingress_cluster_traffic/configuring-ingress-cluster-traffic-ingress-controller.html#nw-ingress-sharding-route-labels_configuring-ingress-cluster-traffic-ingress-controller){: external} you can label routes so that only routers with the matching selector can process traffic for those routes. In the following steps you use router sharding to ensure that the default router processes traffic to routes that have the `router: default` label only. Later, when you create routes that are encrypted with a key that is stored in {{site.data.keyword.hscrypto}}, you use a different route label so that only the HPCS router can process traffic to those routes. The default router in your cluster, which is not integrated with {{site.data.keyword.hscrypto}}, is prevented from processing the encrypted routes.

1. List all existing routes in your cluster.

    ```sh
    oc get routes --all-namespaces
    ```
    {: pre}
    
2. For each route, add a label for the default router.
    1. Edit the route configuration.

        ```sh
        oc edit route <route_name> -n <project>
        ```
        {: pre}

    2. In the `metadata.labels` section, add the `router: default` label.

        ```yaml
        kind: Route
        apiVersion: route.openshift.io/v1
        metadata:
          name: router-default
          namespace: openshift-ingress
          labels:
            ingresscontroller.operator.openshift.io/owning-ingresscontroller: default
            router: default
        spec:
        ...
        ```
        {: codeblock}

3. Save and close the file. Your changes are applied automatically.

4. Edit the configuration for the `IngressController` that manages the default router.

    ```sh
    oc edit IngressController default -n openshift-ingress-operator
    ```
    {: pre}

5. In the `spec` section, add a `routeSelector` section that includes the `router: default` selector.

    ```yaml
    apiVersion: operator.openshift.io/v1
    kind: IngressController
    metadata:
      name: default
      namespace: openshift-ingress-operator
      finalizers:
        - ingresscontroller.operator.openshift.io/finalizer-ingresscontroller
    spec:
      …
      routeSelector:
        matchLabels:
          router: default
    ```
    {: codeblock}

The default router now only processes routes that have the `router: default` label.


## Step 2: Install the {{site.data.keyword.cloud_notm}} HPCS Router operator
{: #addon-operatorhub}

Enable the {{site.data.keyword.cloud_notm}} HPCS Router operator in OperatorHub and install the operator in your cluster.
{: shortdesc}

1. In the [{{site.data.keyword.redhat_openshift_notm}} clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, click the name of the cluster where you want to enable the router.
2. In the **Add-ons** pane, click **Install** on the **{{site.data.keyword.cloud_notm}} HPCS Router Operator** card, and **Install** again to confirm the installation.
3. Click the **OpenShift web console** button.
4. From the side navigation menu in the **Administrator** perspective, click **Operators > OperatorHub**.
5. In the **Provider Type** filter, select the **{{site.data.keyword.cloud_notm}} Router Operators** checkbox. Note that this checkbox might take a few minutes to become available while the add-on finishes installation.
6. Select the **{{site.data.keyword.cloud_notm}} HPCS Router Operator** card, and click **Install**.
7. Select **A specific namespace on the cluster**, select the `openshift-ingress-operator` project from the drop down list, and click **Subscribe**.
8. From the side navigation menu in the **Administrator** perspective, click **Operators > Installed Operators**.
9. Before you continue to the next steps, verify that **Status** for the {{site.data.keyword.cloud_notm}} HPCS Router Operator is `Succeeded`. Note that the operator might take a few minutes to install.

## Step 3: Create and integrate a router with {{site.data.keyword.hscrypto}}
{: #create-hpcs-router}

Use the {{site.data.keyword.cloud_notm}} HPCS Router operator to create a router in your cluster. After you set {{site.data.keyword.hscrypto}} instance data as environment variables for the router, the router can use the `grep11` OpenSSL Engine to access your {{site.data.keyword.hscrypto}} instance.
{: shortdesc}

1. Get the following values for your {{site.data.keyword.hscrypto}} instance:
    * [The service instance ID](/docs/hs-crypto?topic=hs-crypto-retrieve-instance-ID)
    * [The API key for the service instance ID](/docs/account?topic=account-serviceidapikeys#create_service_key)
    * [The `ep11` endpoint URL and port that your service instance uses for key management operations](https://cloud.ibm.com/apidocs/hs-crypto#getinstance)

2. Create a Kubernetes secret named `hpcs-credentials` that contains the values that you retrieved. The HPCS router uses the environment variables in this secret to authenticate with your {{site.data.keyword.hscrypto}} instance.

    ```yaml
    kind: Secret
    apiVersion: v1
    metadata:
        name: hpcs-credentials
    namespace: openshift-ingress
    stringData:
      LIBGREP11_CONNECTION_ADDRESS: <ep11_endpoint_URL>
      LIBGREP11_CONNECTION_PORT: "<ep11_endpoint_port>"
      LIBGREP11_IAMAUTH_APIKEY: <service_instance_ID_API_key>
      LIBGREP11_IAMAUTH_INSTANCEID: <service_instance_ID>
    type: Opaque
    ```
    {: screen}

    Example

    ```yaml
    kind: Secret
    apiVersion: v1
    metadata:
      name: hpcs-credentials
    namespace: openshift-ingress
    stringData:
      LIBGREP11_CONNECTION_ADDRESS: ep11.us-south.hs-crypto.cloud.ibm.com
      LIBGREP11_CONNECTION_PORT: "9371"
      LIBGREP11_IAMAUTH_APIKEY: AAaa11BBbb22CCcc33DDdd44EEee55FFff66GGgg77-0
      LIBGREP11_IAMAUTH_INSTANCEID: 1234abcd-56ef-78gh-90ij-1234klmn5678
    type: Opaque
    ```
    {: screen}

3. Create the secret in the `openshift-ingress` project.

    ```sh
    oc create -f hpcs-credentials.yaml -n openshift-ingress
    ```
    {: pre}

4. To create the router, create an `HPCSIngressController` custom resource that contains the `router: hpcs` selector for router sharding. For the router name, consider using the name of your {{site.data.keyword.hscrypto}} instance for easy identification.

    ```yaml
    apiVersion: operator.roks.cloud.ibm.com/v1
    kind: HPCSIngressController
    metadata:
      name: <router_name>
    namespace: openshift-ingress
    spec:
      routeSelector:
        matchLabels:
          router: hpcs
    ```
    {: codeblock}

5. Deploy the `HPCSIngressController` custom resource into the `openshift-ingress` project. When this router is deployed, the operator automatically creates a Kubernetes load balancer service to expose the router deployment. In multizone classic clusters, one load balancer is created in every zone. In multizone VPC clusters, one load balancer that process traffic for every zone is created.

    ```sh
    oc create -n openshift-ingress -f <router_name>.yaml
    ```
    {: pre}

6. Get the IP address (classic) or hostname (VPC) of each load balancer service that is named in the format `hpcs-router-<router_name>-<zone>`.

    ```sh
    oc get svc -n openshift-ingress
    ```
    {: pre}

7. Register the IP address (classic) or hostname (VPC) of each load balancer with a DNS entry by creating a subdomain for your {{site.data.keyword.cloud_notm}} HPCS router.
    * **IBM-provided domain**: If you don't need to use a custom domain, you can generate an IBM-provided subdomain.

        * ![Classic](../icons/classic.svg "Classic") Classic:

            ```sh
            ibmcloud oc nlb-dns create classic --cluster <cluster_name_or_ID> --ip LB_IP [--ip LB2_IP --ip LB3_IP]
            ```
            {: pre}

        * ![VPC](../icons/vpc.svg "VPC") VPC:

            ```sh
            ibmcloud oc nlb-dns create vpc-gen2 --cluster <cluster_name_or_ID> --lb-host <LB_hostname>
            ```
            {: pre}

    * **Custom domain**: Create a custom domain with your DNS provider or [{{site.data.keyword.cis_full}}](https://cloud.ibm.com/catalog/services/internet-services), and add the load balancer IP address as an A record (classic) or the load balancer hostname as a CNAME (VPC).

8. Add the domain to the router deployment by editing the `HPCSIngressController` custom resource.

    ```sh
    oc edit -n openshift-ingress hpcsingresscontrollers.operator.roks.cloud.ibm.com <router_name>
    ```
    {: pre}

9. In the `spec` section, add the `domain` section and specify your domain.

    ```yaml
    apiVersion: operator.roks.cloud.ibm.com/v1
    kind: HPCSIngressController
    metadata:
      name: <router_name>
    namespace: openshift-ingress
    spec:
      routeSelector:
        matchLabels:
          router: hpcs
      domain:
        <domain>
    ```
    {: codeblock}

10. Save and close the file. Your changes are applied automatically.

## Step 4: Create a route certificate that uses a private key from {{site.data.keyword.hscrypto}}
{: #generate-csr}

Use the {{site.data.keyword.cloud_notm}} HPCS Router operator to generate and sign a Certificate Signing Request (CSR) with a private key that is stored in {{site.data.keyword.hscrypto}}. You can then send the CSR to a certificate authority to get a certificate for your domain.
{: shortdesc}

1. Create a `Certificate` custom resource that specifies details for the CSR, such as the domain that you previously created.

    ```yaml
    apiVersion: operator.roks.cloud.ibm.com/v1
    kind: Certificate
    metadata:
      # A name for the CSR to be generated
      name: <CSR_name>
      # The project where you want to create routes for your apps
      namespace: <project>
    spec:
      dnsNames:
      # The domain that you registered in step 7 of the previous section
      - <domain>
      # Optional: Any alternative DNS names for this domain
      - <alternative_domain_name>
      isCA: false
      privateKey:
        algorithm: ECDSA
        size: 256
      # A name for the secret to be generated, containing the CSR and keys
      secretName: <secret_name>
      subject:
        organizations:
          # Optional: A list of organization names to be used on the certificate
          - <organization_name>
      usages:
        - server auth
        - client auth
    ```
    {: codeblock}

2. Create the `Certificate` custom resource.

    ```sh
    oc create -f <CSR_name>.yaml -n <project>
    ```
    {: pre}

    When this resource is created, the following processes occur:
      * {{site.data.keyword.cloud_notm}} HPCS Router operator creates a CSR generator job and a `ConfigMap` resource.
      * The CSR generator job uses the `ConfigMap` to process the data in the `Certificate` custom resource.
      * The CSR generator job uses the data in the `Certificate` custom resource and the credentials in the `hpcs-credentials` secret to sign the CSR.
      * A secret that contains the signed CSR, the `grep11` reference to the generated private key, and the generated public key is created in the project that you specified in the `Certificate` custom resource.

3. Get the signed CSR from the generated secret. Additionally, note the `grep11` reference to the generated private key, which is used in a later step.

    ```sh
    oc get secret <secret_name> -n <project> -o yaml
    ```
    {: pre}

4. Send the CSR to your preferred certificate authority to obtain a certificate for your router domain.

## Step 5: Create an encrypted route with the certificate
{: #create-route}

After you obtain the certificate from your certificate authority, use the certificate and the `grep11` reference to the generated private key to create an encrypted route that exposes your app.
{: shortdesc}

1. Create a `Route` resource. Specify the certificate and the `grep11` reference to the generated private key from the generated CSR secret.

    ```yaml
    kind: Route
    apiVersion: route.openshift.io/v1
    metadata:    
      # A name for the route to be generated
      name: <route_name>
      # The project where the CSR secret was generated
      namespace: <project>
      labels:
        router: hpcs
    spec:
        host:
        # The router domain that you registered
        <domain>
        to:
        kind: Service
        # The name of the clusterIP service that exposes your app
        name: <app_service_name>
        weight: 100
        port:
        targetPort: https
        tls:
        termination: edge
        # The contents of the certificate
        certificate: |-
            -----BEGIN CERTIFICATE-----
            <cert>
            -----END CERTIFICATE-----
        # The reference to the private key
        key: |-
            -----BEGIN PRIVATE KEY-----
            <grep11_ref_to_private_key>
            -----END PRIVATE KEY-----
        # Optional: the CA certificate
        caCertificate: |-
            -----BEGIN CERTIFICATE-----
            <optional_ca_cert>
            -----END CERTIFICATE-----
        insecureEdgeTerminationPolicy: Redirect
        wildcardPolicy: None
    ```
    {: codeblock}

2. Create the route. Because the route is labeled with `router: hpcs`, only the {{site.data.keyword.cloud_notm}} HPCS Router processes traffic for the route.

    ```sh
    oc create -f <route_name>.yaml -n <project>
    ```
    {: pre}

3. Verify that the route for your app is created.

    ```sh
    oc get routes
    ```
    {: pre}

4. Verify that the TLS session is correctly established by making `https` calls to your app's route.

5. Optional: Customize routing rules with [optional configurations](https://docs.openshift.com/container-platform/4.9/networking/routes/route-configuration.html){: external}. For example, you can use [route-specific HAProxy annotations](https://docs.openshift.com/container-platform/4.9/networking/routes/route-configuration.html#nw-route-specific-annotations_route-configuration){: external}.

## Version history
{: #hpcs-versions}

For the list of changes for each {{site.data.keyword.cloud_notm}} HPCS Router add-on version, see the [{{site.data.keyword.cloud_notm}} HPCS Router add-on changelog](/docs/openshift?topic=openshift-hpcs-router-changelog).






