---

copyright:
  years: 2014, 2020
lastupdated: "2020-12-02"

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
{:vb.net: .ph data-hd-programlang='vb.net'}
{:video: .video}



# Setting up Kubernetes Ingress
{: #ingress-types}

<img src="images/icon-version-311.png" alt="Version 3.11 icon" width="30" style="width:30px; border-style: none"/> This information is for clusters that run {{site.data.keyword.openshiftshort}} version 3.11 only. To learn about Ingress for {{site.data.keyword.openshiftshort}} version 4, see [About Ingress in {{site.data.keyword.openshiftshort}} version 4 or later](/docs/openshift?topic=openshift-ingress-about-roks4).
{: important}

As of 01 December 2020, {{site.data.keyword.openshiftlong_notm}} primarily supports the Kubernetes Ingress image for the Ingress application load balancers (ALBs) in your cluster. The Kubernetes Ingress image is built on the community Kubernetes project's implementation of the NGINX Ingress controller. The previously supported {{site.data.keyword.openshiftlong_notm}} Ingress image, which was built on a custom implementation of the NGINX Ingress controller, is deprecated.
{: shortdesc}

**Clusters created on or after 01 December 2020**: Default application load balancers (ALBs) run the Kubernetes Ingress image in all new {{site.data.keyword.openshiftlong_notm}} clusters that run version 3.11.

**Clusters created before 01 December 2020**:
* Existing clusters with ALBs that run the custom IBM Ingress image continue to operate as-is.
* Support for the custom IBM Ingress image ends in 6 months on 30 April 2021.
* You must move to the new Kubernetes Ingress by migrating any existing Ingress setups. Your existing ALBs and other Ingress resources are not automatically migrated to the new Kubernetes Ingress image.
* You can easily migrate to Kubernetes Ingress by using the [migration tool](/docs/openshift?topic=openshift-ingress-types#alb-type-migration) that is developed and supported by IBM Cloud Kubernetes Service.
* If you do not move to Kubernetes Ingress before 30 April 2020, ALBs that run the custom IBM Ingress image continue to run, but all support from IBM Cloud for those ALBs is discontinued.

Not ready to switch your ALBs to the Kubernetes Ingress image yet? When you enable or update an existing ALB, the ALB continues to run the same image that the ALB previously ran: either the Kubernetes Ingress image or the {{site.data.keyword.openshiftlong_notm}} Ingress image. Your existing ALBs do not begin to run the Kubernetes Ingress image until you specify the Kubernetes Ingress image version in the `--version` flag when you enable them.
{: tip}

For a comparison of the Kubernetes Ingress image and the deprecated IBM Ingress image, review the following tables.

## Comparison of the ALB image types
{: #about-alb-images}

Review the following similarities are differences between the {{site.data.keyword.openshiftlong_notm}} Ingress and the Kubernetes Ingress images.
{: shortdesc}

### Similarities between Ingress images
{: #alb-image-same}

Review the following similarities between the {{site.data.keyword.openshiftlong_notm}} Ingress and the Kubernetes Ingress images.
{: shortdesc}

|Characteristic|Comparison|
|--------------|----------|
|Ingress components| Regardless of which image type your ALBs use, [Ingress still consists of the same three components](/docs/openshift?topic=openshift-ingress-about#ingress_components) in your cluster: Ingress resources, application load balancers (ALBs), and the multizone load balancer (MZLB).|
|Traffic flow| Both ALB images implement the NGINX Ingress controller. In that sense, [the way that ALBs function in your cluster to route traffic to your apps](/docs/openshift?topic=openshift-ingress-about#architecture-classic) is similar for both image types.|
|ALB management| The image type does not affect how you manage the lifecycle of ALBs in your cluster. All ALBs can be managed by using `ibmcloud oc ingress alb` CLI commands. Additionally, IBM manages the [automatic updates of ALB versions](/docs/containers?topic=containers-ingress-types#alb-update). |
{: caption="Similarities between Ingress images"}

### Differences between Ingress images
{: #alb-image-diff}

Review the following important differences between the {{site.data.keyword.openshiftlong_notm}} Ingress and the Kubernetes Ingress images.
{: shortdesc}

|Characteristic|Custom {{site.data.keyword.openshiftlong_notm}} image|Kubernetes image|
|--------------|----------------------------|--------------------|
|Annotation class| Only [custom {{site.data.keyword.openshiftlong_notm}} annotations](/docs/openshift?topic=openshift-ingress_annotation) (`ingress.bluemix.net/<annotation>`) are supported. | Only [Kubernetes NGINX annotations](/docs/openshift?topic=openshift-comm-ingress-annotations#annotations){: external} (`nginx.ingress.kubernetes.io/<annotation>`) are supported.|
|Annotation application to services| Within the annotation, you can specify the app service name that you want to apply the annotation to. | Annotations are always applied to all service paths in the resource, and you cannot specify service names within the annotations.|
|Protocols| HTTP/2 and gRPC protocols are not supported.|HTTP/2 and gRPC protocols are supported.|
|TLS secrets| The ALB can access a TLS secret in the `default` project, in the `ibm-cert-store` project, or in the same project where you deploy the Ingress resource.| The ALB can access a TLS secret in the same project where you deploy the Ingress resource only, and cannot access secrets in any other projects.|
{: caption="Differences between Ingress images"}

<br />

## Exposing apps with ALBs that run the Kubernetes Ingress image
{: #alb-comm-create}

Create Ingress resources so that ALBs that run the community Kubernetes Ingress image can route traffic to your apps.
{: shortdesc}

The following steps show you how to expose your apps with the Kubernetes Ingress setup. If you created your cluster on or after 01 December 2020, your ALBs run the Kubernetes Ingress image by default. However, if you created your cluster before 01 December 2020, your ALBs run the deprecated custom IBM Ingress image. In this case, you can use the following steps to create new ALBs that run the Kubernetes Ingress image, and run this new Kubernetes Ingress setup alongside your existing IBM Ingress setup. If you prefer to migrate your existing IBM Ingress setup to the Kubernetes Ingress setup instead, check out [Migrating your existing Ingress ALB setup to run Kubernetes Ingress](#alb-type-migration).
{: tip}

1. To use TLS termination, re-create your TLS secrets. In the Kubernetes Ingress implementation, the ALB cannot access secrets that are in a different project than the Ingress resource. If you use the default Ingress secret and your Ingress resources are deployed in projects other than `default`, or if you import a secret from {{site.data.keyword.cloudcerts_long_notm}} and your Ingress resources are deployed in projects other than `ibm-cert-store`, you must re-create the secret in those projects. For more information, see [Managing TLS certificates and secrets](#manage_certs).
    1. Get the CRN of the secret for your subdomain.
      ```
      ibmcloud oc ingress secret get -c <cluster> --name <secret_name> --namespace default
      ```
      {: pre}
    2. Using the CRN, create a secret for the certificate in the project where your Ingress resources are deployed. If you have Ingress resources in multiple projects, repeat this command for each project.
      ```
      ibmcloud oc ingress secret create --cluster <cluster_name_or_ID> --cert-crn <CRN> --name <secret_name> --namespace project
      ```
      {: pre}

2. Create an Ingress resource that is formatted for use with ALBs that run the Kubernetes Ingress image.
  1. Define an Ingress resource file that uses the IBM-provided domain or your custom domain to route incoming network traffic to the services that you created earlier.
     ```yaml
     apiVersion: extensions/v1beta1
     kind: Ingress
     metadata:
       name: community-ingress-resource
       annotations:
         kubernetes.io/ingress.class: "<public|private>-iks-k8s-nginx"
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
      <td><code>annotations</code></td>
      <td><ul><li>`kubernetes.io/ingress.class`: Specify `public-iks-k8s-nginx` or `private-iks-k8s-nginx` to apply this Ingress resource to the public ALBs or private ALBs that run the Kubernetes Ingress image in your cluster.<p class="note">For configurations in which another component manages your Ingress ALBs, such as if Ingress is deployed as part of a Helm chart, do not specify this annotation. Instead, you can specify your own class in a `spec.spec.ingressClassName: :<class_name>` field. You must also specify this custom class in an [`IngressClass` resource and a `ibm-ingress-deploy-config` configmap](#ingress-class).</p></li><li>To customize routing for Ingress, you can add [Kubernetes NGINX annotations](/docs/openshift?topic=openshift-comm-ingress-annotations#annotations) (`nginx.ingress.kubernetes.io/<annotation>`). Custom {{site.data.keyword.openshiftlong_notm}} annotations (`ingress.bluemix.net/<annotation>`) are **not** supported.</li></ul></td>
      </tr>
      <tr>
      <td><code>tls.hosts</code></td>
      <td>To use TLS, replace <em>&lt;domain&gt;</em> with the IBM-provided Ingress subdomain or your custom domain.</td>
      </tr>
      <tr>
      <td><code>tls.secretName</code></td>
      <td>Replace <em>&lt;tls_secret_name&gt;</em> with the name of the TLS secret for your domain.<td>
      </tr>
      <tr>
      <td><code>host</code></td>
      <td>Replace <em>&lt;domain&gt;</em> with the IBM-provided Ingress subdomain or your custom domain.</td>
      </tr>
      <tr>
      <td><code>path</code></td>
      <td>Replace <em>&lt;app_path&gt;</em> with a slash or the path that your app is listening on. The path is appended to the IBM-provided or your custom domain to create a unique route to your app. When you enter this route into a web browser, network traffic is routed to the ALB. The ALB looks up the associated service and sends network traffic to the service. The service then forwards the traffic to the pods where the app runs.</td>
      </tr>
      <tr>
      <td><code>serviceName</code></td>
      <td>Replace <em>&lt;app1_service&gt;</em> and <em>&lt;app2_service&gt;</em>, and so on, with the name of the services you created to expose your apps.</td>
      </tr>
      <tr>
      <td><code>servicePort</code></td>
      <td>The port that your service listens to. Use the same port that you defined when you created the Kubernetes service for your app.</td>
      </tr>
      </tbody></table>

  2.  Create the Ingress resource for your cluster. Ensure that the resource deploys into the same namespace as the app services that you specified in the resource.
      ```
      oc apply -f community-ingress-resource.yaml -n <namespace>
      ```
      {: pre}

3. Clusters created before 01 December 2020: Verify that you have at least one ALB in each zone that runs the Kubernetes Ingress image. In the **Build** column of the output, look for versions in the `<community_version>_<ibm_build>_iks` Kubernetes Ingress format.
      ```
      ibmcloud oc alb ls -c <cluster_name_or_ID>
      ```
      {: pre}

      * If one ALB per zone runs the Kubernetes Ingress image, continue to step 4.
      * If you do not have one ALB per zone that runs the Kubernetes Ingress image, create at least one in each zone.
          ```
          ibmcloud oc ingress alb create classic --cluster <cluster_name_or_ID> --type <public_or_private> --zone <zone> --vlan <VLAN_ID> --version 0.35.0_474_iks
          ```
          {: pre}

4. Copy the IP address for one ALB that runs the Kubernetes Ingress image. In the output, choose an ALB that has a **Build** in the format `<community_version>_<ibm_build>_iks`.
  ```
  ibmcloud oc ingress alb ls -c <cluster>
  ```
  {: pre}

5. Using the ALB's IP address, the app path, and your domain, verify that you can successfully send traffic to your app through this ALB.
  ```
  curl http://<ALB_IP>/<app_path> -H "Host: <ingress_subdomain>"
  ```
  {: pre}

  For example, to send a request to "myapp" by using a default Ingress subdomain:
  ```
  curl http://8.8.8.8/myapp -H "Host: mycluster-a1b2cdef345678g9hi012j3kl4567890-0000.us-south.containers.appdomain.cloud"
  ```
  {: pre}

<br />

## Migrating your existing Ingress ALB setup to run Kubernetes Ingress
{: #alb-type-migration}

Change your ALBs from the {{site.data.keyword.openshiftlong_notm}} Ingress image to the Kubernetes Ingress image.
{: shortdesc}

The following steps use the Ingress resource migration tool to help you create Ingress resources, including annotations, for the Kubernetes Ingress format. The migration tool also creates a new configmap resource that is formatted for the Kubernetes Ingress implementation. Then, you change the version of your ALBs to use the community Kubernetes Ingress image.

The migration tool is intended to help you prepare your Ingress resources and configmap. However, you must verify, test, and modify your Ingress resources and configmap to ensure that they work correctly with the Kubernetes Ingress image.
{: important}

### Step 1: Copy TLS secrets
{: #alb-migrate-1}

To use TLS termination, re-create your TLS secrets.
{: shortdesc}

In the Kubernetes Ingress implementation, the ALB cannot access secrets that are in a different project than the Ingress resource. If you use the default Ingress secret and your Ingress resources are deployed in projects other than `default`, or if you import a secret from {{site.data.keyword.cloudcerts_long_notm}} and your Ingress resources are deployed in projects other than `ibm-cert-store`, you must re-create the secret in those projects. For more information, see [Managing TLS certificates and secrets](#manage_certs).

1. Get the CRN of the Ingress secret for your default Ingress subdomain. To get the name of the default secret, run `ibmcloud oc cluster get -c <cluster> | grep Ingress`.
  ```
  ibmcloud oc ingress secret get -c <cluster> --name <secret_name> --namespace default
  ```
  {: pre}
2. Using the CRN, create a secret for the certificate in the project where your Ingress resources are deployed. If you have Ingress resources in multiple projects, repeat this command for each project.
  ```
  ibmcloud oc ingress secret create --cluster <cluster_name_or_ID> --cert-crn <CRN> --name <secret_name> --namespace project
  ```
  {: pre}

### Step 2: Update Ingress resources
{: #alb-migrate-2}

1. Run a test of the migration tool for public Ingress routing (`--type test`) or private Ingress routing (`--type test-with-private`). When you run a test migration, the following objects are created:
    * A test ALB service:
      * Runs the Kubernetes Ingress image
      * Uses the `test` class
      * Is registered with a test version of your Ingress subdomain, such as `mycluster-a1b2cdef345678g9hi012j3kl4567890-m000.us-south.containers.appdomain.cloud`
    * Copies of your Ingress resources:
      * Use the `test` Ingress class
      * Contain annotations that are transformed into the Kubernetes NGINX format
      * For each subdomain in your Ingress resource file, a subdomain based on the test Ingress subdomain is created. For example, if you list `example.com` in your Ingress resource, the subdomain `example-com-123456.mycluster-a1b2cdef345678g9hi012j3kl4567890-m000.us-south.containers.appdomain.cloud` is created in the test copy.
      * If your Ingress resource files included TLS sections, a secret for the test subdomain is also created and is listed in the test copies.
      * If your Ingress resource files defined more than one service per file, multiple test copies are created so that only one service is defined per file.
    * A test configmap:
      * Formatted for the Kubernetes Ingress implementation
      * Includes any fields that you configured in the `ibm-cloud-provider-ingress-cm` configmap

  ```
  ibmcloud oc ingress alb migrate start --type (test | test-with-private) -c <cluster_name_or_ID>
  ```
  {: pre}

2. Verify that the **Status** of the migration is `completed`.
  ```
  ibmcloud oc ingress alb migrate status -c <cluster_name_or_ID>
  ```
  {: pre}

  * If the **Status** is `failed`:
    1. Check the logs for the migration.
        ```
        oc logs -n kube-system job/ingress-migration
        ```
        {: pre}
    2. [Open a support case](/docs/openshift?topic=openshift-get-help#help-support) and include the migration job logs in your case.

3. In the output of the previous step, review the **Resource migrations warnings** for each Ingress resource or configmap. These messages indicate fields or configurations, such as annotations, that were not migrated, and the steps to manually change the field for compatibility with the Kubernetes Ingress implementation. To resolve warnings, edit the manifest for each resource or configmap.<p class="important">Some differences between the images cannot be migrated by this tool and must be migrated manually. To see a comparison between annotations for each image type, see [Customizing Kubernetes Ingress routing with annotations and configmaps](/docs/openshift?topic=openshift-comm-ingress-annotations#annotations).</p>
  * Ingress resources:
    ```
    oc edit ingress <migrated_resource_name> -n <namespace>
    ```
    {: pre}
  * Configmap:
    ```
    oc edit cm ibm-k8s-controller-config-test -n kube-system
    ```
    {: pre}
  * Test ALB service:
    ```
    oc edit deployment public-ingress-migrator -n kube-system
    ```
    {: pre}

4. Try to send a traffic request to your apps by accessing the test subdomain and each of your app paths.
    * If your Ingress resources include TLS:
      ```
      https://test-<ingress_subdomain>/<app1_path>
      ```
      {: codeblock}
    * If your Ingress resources do not include TLS:
      ```
      http://test-<ingress_subdomain>/<app1_path>
      ```
      {: codeblock}

5. After you verify that your test Ingress system is working properly, make local copies of your changes to the test Ingress resources, test configmap, and test ALB service. When you run the migration tool in production, any previously generated test resources are overwritten, and any changes that you made to your test copies must also be made for the production copies. Locally retaining any changes you made to your test copies can help you quickly make changes to your production copies.

6. Optional: After you copy your changes, clean up the test resources.
  * Test Ingress resource copies:
    ```
    ibmcloud oc ingress alb migrate clean -c <cluster_name_or_ID> --test-ingresses -f
    ```
    {: pre}
  * Test configmap:
    ```
    oc delete cm ibm-k8s-controller-config-test -n kube-system
    ```
    {: pre}
  * Test ALB service:
    ```
    oc delete service public-ingress-migrator -n kube-system
    ```
    {: pre}

7. Run the migration tool in production. Your previous test resources are overwritten with a new set of production resources. After the migration is complete, no changes are made in production until you change the image type of your ALBs in subsequent steps.
  ```
  ibmcloud oc ingress alb migrate start --type production -c <cluster_name_or_ID>
  ```
  {: pre}

8. Check the status of the migration to verify that the production migration is complete.
  ```
  ibmcloud oc ingress alb migrate status -c <cluster_name_or_ID>
  ```
  {: pre}

9. If you made changes to your test copies in step 3, make these changes again in the production version of these copies.
  * Ingress resources:
    ```
    oc edit ingress <migrated_resource_name> -n <namespace>
    ```
    {: pre}
  * Configmap:
    ```
    oc edit cm ibm-k8s-controller-config-test -n kube-system
    ```
    {: pre}
  * To make any changes to the ALB services, such as to open non-standard ports, continue to the next section.

### Step 3: Change ALB images
{: #alb-migrate-3}

Decide whether to [create new ALBs](#alb-migrate-3-new) that run Kubernetes Ingress, or to [migrate your existing ALBs](#alb-migrate-3-existing) to use the Kubernetes Ingress image. If you do not have a specific requirement to keep your existing ALBs, you can prevent downtime by creating new ALBs.
{: shortdesc}

#### Create new ALBs
{: #alb-migrate-3-new}

Create new ALBs that run the Kubernetes Ingress image. After you create the new ALBs, you can either delete the old ALBs that run the {{site.data.keyword.openshiftlong_notm}} Ingress image, or you can run the new Kubernetes Ingress ALBs and old {{site.data.keyword.openshiftlong_notm}} Ingress ALBs alongside each other in your cluster.
{: shortdesc}

1. Optional: To continue running old {{site.data.keyword.openshiftlong_notm}} Ingress ALBs alongside any new Kubernetes Ingress ALBs in your cluster, add the `kubernetes.io/ingress.class: "iks-nginx"` annotation to any Ingress resource that you want to apply only to the ALBs that run {{site.data.keyword.openshiftlong_notm}} Ingress. This annotation ensures that your existing Ingress resources are applied only to the {{site.data.keyword.openshiftlong_notm}} Ingress ALBs, while the `kubernetes.io/ingress.class: "<public|private>-iks-k8s-nginx"` annotations in your migrated Ingress resources ensure that they are applied only to the new Kubernetes Ingress ALBs that you create.
    ```
    oc edit ingress <ingress_resource>
    ```
    {: pre}

2. <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Optional for classic clusters: If you do not want traffic to immediately be routed to the ALBs that you create in the next step, you can first remove the new ALBs from the DNS registration for the ALB health check subdomain.
  1. Open the health check resource for ALBs that run the Kubernetes Ingress image.
    ```
    kubectl edit ing k8s-alb-health -n kube-system
    ```
    {: pre}
  2. In the `spec.rules` section, change the `host` by adding any character to the health subdomain. For example, if the health subdomain is listed as `albhealth.mycluster.us-south.containers.appdomain.cloud`, you could add a `x` to the subdomain such as `xalbhealth.mycluster.us-south.containers.appdomain.cloud`. The added character ensures that the Cloudflare health check that uses this subdomain fails, and that any IP addresses for ALBs that run the Kubernetes Ingress image are consequently removed from the DNS registration for your Ingress subdomain. Because your ALBs that run the {{site.data.keyword.openshiftlong_notm}} use a different health check resource than this resource, they continue to receive traffic. After you test your new ALBs in subsequent steps, you can remove the added character to ensure that the new ALBs are included in the DNS registration again.
  3. Save and close the file. Your changes are applied automatically.

3. Choose the version for Kubernetes Ingress image that you want to use.<p class="note">To choose a version other than the default, you must first disable automatic updates by running the `ibmcloud oc ingress alb autoupdate disable` command.</p>
  ```
  ibmcloud oc ingress alb versions
  ```
  {: pre}

4. Create at least one ALB in each zone that runs the Kubernetes Ingress image. These ALBs read only the Ingress resources and configmap that are formatted for Kubernetes Ingress, and begin to forward traffic according to those resources.<p class="note"><img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> In VPC clusters, one VPC load balancer exposes all ALBs in your cluster. When you run one of the following commands to create an ALB, the new ALB immediately begins to receive traffic that is routed by the VPC load balancer. Consider creating only one ALB that runs the Kubernetes Ingres image and testing that ALB in the following steps before you create more ALBs.</p>
    ```
    ibmcloud oc ingress alb create classic --cluster <cluster_name_or_ID> --type <public_or_private> --zone <zone> --vlan <VLAN_ID> --version <version>
    ```
    {: pre}

5. Verify that the new ALBs are created.
  ```
  ibmcloud oc ingress alb ls -c <cluster>
  ```
  {: pre}

6. If you made any changes to the test ALB service during your test migration, such as opening non-standard ports, make those changes to these ALB services.
  ```
  oc edit -n kube-system svc <ALB_ID>
  ```
  {: pre}

7. Copy the IP address for one ALB that has the Kubernetes Ingress version that you specified in the **Build** column, such as `0.35.0_474_iks`.
  ```
  ibmcloud oc ingress alb ls -c <cluster>
  ```
  {: pre}

8. Using the ALB's IP address, the app path, and your domain, verify that you can successfully send traffic to your app through this ALB.
  ```
  curl http://<ALB_IP>/<app_path> -H "Host: ingress.subdomain.containers.appdomain.cloud"
  ```
  {: pre}

  For example, to send a request to "myapp" by using a default Ingress subdomain:
  ```
  curl http://8.8.8.8/myapp -H "Host: mycluster-a1b2cdef345678g9hi012j3kl4567890-0000.us-south.containers.appdomain.cloud"
  ```
  {: pre}

9. <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Optional for classic clusters: If you changed the ALB health check subdomain in step 2, remove the added character to ensure that the new ALBs are included in the DNS registration again.
  1. Open the health check resource for ALBs that run the Kubernetes Ingress image.
    ```
    kubectl edit ing k8s-alb-health -n kube-system
    ```
    {: pre}
  2. In the `spec.rules` section, change the `host` by removing the extra character from the health subdomain. The Cloudflare health check for this subdomain can now resume, and the IP addresses for the new ALBs are added back to the DNS registration.
  3. Save and close the file. Your changes are applied automatically.

10. Optional: If you do not want to run the new Kubernetes Ingress ALBs alongside the old {{site.data.keyword.openshiftlong_notm}} Ingress ALBs, remove the old {{site.data.keyword.openshiftlong_notm}} Ingress ALBs and clean up your original Ingress resource files that were formatted for the {{site.data.keyword.openshiftlong_notm}} Ingress image.
  * Original ALBs that run the {{site.data.keyword.openshiftlong_notm}} Ingress image:
    1. List your ALB IDs. In the output, copy the IDs for ALBs that have the {{site.data.keyword.openshiftlong_notm}} Ingress version in the **Build** column, such as `653`.
      ```
      ibmcloud oc ingress alb ls -c <cluster>
      ```
      {: pre}

    2. Disable each of the old ALBs.
      ```
      ibmcloud oc ingress alb disable --alb <ALB_ID> -c <cluster_name_or_ID>
      ```
      {: pre}

  * Original {{site.data.keyword.openshiftlong_notm}} Ingress resources:
    ```
    ibmcloud oc ingress alb migrate clean -c <cluster_name_or_ID> --iks-ingresses -f
    ```
    {: pre}
  * Original {{site.data.keyword.openshiftlong_notm}} Ingress configmap:
    ```
    oc delete cm ibm-cloud-provider-ingress-cm -n kube-system
    ```
    {: pre}

11. If you use {{site.data.keyword.blockchainfull}}, you must [re-establish connectivity between the {{site.data.keyword.blockchain}} management console and your cluster](/docs/blockchain?topic=blockchain-ibp-console-manage-console#ibp-console-refresh).

#### Migrate existing ALBs
{: #alb-migrate-3-existing}

If you choose to change your existing ALBs to the Kubernetes Ingress image, an ALB must first be disabled, and traffic to your apps might be disrupted. Make sure that you have at least two worker nodes per zone or [add more ALBs in a zone](#create_alb) so that other ALBs can continue to route traffic while one ALB is disabled at a time.
{: important}

1. Change the image type of one ALB to test traffic flow. When you change the ALB's image type, the ALB now only reads the Ingress resources and configmap that are formatted for Kubernetes Ingress, and begins to forward traffic according to those resources.
    1. List your ALB IDs. In the output, copy the ID and IP address for one ALB.
      ```
      ibmcloud oc ingress alb ls -c <cluster>
      ```
      {: pre}

    2. Disable the ALB.
      ```
      ibmcloud oc ingress alb disable --alb <ALB_ID> -c <cluster_name_or_ID>
      ```
      {: pre}

    3. Before continuing to the next step, verify that the ALB IP address is removed from the DNS registration for the Ingress subdomain.
      ```
      nslookup <ingress_subdomain>
      ```
      {: pre}

    4. Choose the version for Kubernetes Ingress image that you want to use.<p class="note">To choose a version other than the default, you must first disable automatic updates by running the `ibmcloud oc ingress alb autoupdate disable` command.</p>
      ```
      ibmcloud oc ingress alb versions
      ```
      {: pre}

    5. Re-enable the ALB. Specify the image version that you chose in the `--version` flag.
        ```
        ibmcloud oc ingress alb enable classic --alb <ALB_ID> -c <cluster_name_or_ID> --version <image_version>
        ```
        {: pre}

    6. If you made any changes to the test ALB service during your test migration, such as opening non-standard ports, make those changes to this ALB service.
      ```
      oc edit -n kube-system svc <ALB_ID>
      ```
      {: pre}

    7. Using the ALB's IP address, the app path, and your domain, verify that you can successfully send traffic to your app through this ALB.
      ```
      curl http://<ALB_IP>/<app_path> -H "Host: ingress.subdomain.containers.appdomain.cloud"
      ```
      {: pre}

      For example, to send a request to "myapp" by using a default Ingress subdomain:
      ```
      curl http://8.8.8.8/myapp -H "Host: mycluster-a1b2cdef345678g9hi012j3kl4567890-0000.us-south.containers.appdomain.cloud"
      ```
      {: pre}

    8. After you verify that traffic is flowing correctly through one ALB, repeat these steps for each ALB in your cluster. <p class="note">To ensure that the implementation of Ingress is consistent across your apps, make sure that you change the image for all of your ALBs in the cluster.</p>

2. Optional: Clean up your original Ingress resource files that were formatted for the {{site.data.keyword.openshiftlong_notm}} Ingress image.
  * Original {{site.data.keyword.openshiftlong_notm}} Ingress resources:
    ```
    ibmcloud oc ingress alb migrate clean -c <cluster_name_or_ID> --iks-ingresses -f
    ```
    {: pre}
  * Original {{site.data.keyword.openshiftlong_notm}} Ingress configmap:
    ```
    oc delete cm ibm-cloud-provider-ingress-cm -n kube-system
    ```
    {: pre}

3. If you use {{site.data.keyword.blockchainfull}}, you must [re-establish connectivity between the {{site.data.keyword.blockchain}} management console and your cluster](/docs/blockchain?topic=blockchain-ibp-console-manage-console#ibp-console-refresh).

<br />

## Managing TLS certificates and secrets
{: #manage_certs}

As of 24 August 2020, an [{{site.data.keyword.cloudcerts_long}}](/docs/certificate-manager?topic=certificate-manager-about-certificate-manager) instance is automatically created for each cluster that you can use to manage the cluster's Ingress TLS certificates.
{: shortdesc}

For an {{site.data.keyword.cloudcerts_short}} instance to be created for your new or existing cluster, ensure that the API key for the region and resource group that the cluster is created in has the correct permissions.
* If the account owner set the API key, then your cluster is assigned an {{site.data.keyword.cloudcerts_short}} instance.
* If another user or a functional ID set the API key, first [assign the user](/docs/openshift?topic=openshift-users#add_users) the **Administrator** or **Editor** platform role _and_ the **Manager** service role for {{site.data.keyword.cloudcerts_short}} in **All resource groups**. Then, the user must [reset the API key for the region and resource group](/docs/openshift?topic=openshift-users#api_key_most_cases). After the cluster has access to the updated permissions in the API key, your cluster is automatically assigned an {{site.data.keyword.cloudcerts_short}} instance.

When the creation of the {{site.data.keyword.cloudcerts_short}} instance is triggered, the {{site.data.keyword.cloudcerts_short}} instance might take up to an hour to become visible in the {{site.data.keyword.cloud_notm}} console.
{: note}

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

In the Kubernetes Ingress implementation, ALBs can access TLS secrets only in the same project that the Ingress resource is deployed to. If your Ingress resources are deployed in projects other than `default`, you must create a secret for the default TLS certificate in those projects by running `ibmcloud oc ingress secret create --cluster <cluster_name_or_ID> --cert-crn <CRN> --name <secret_name> --namespace project` in each project.
{: note}

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

3. Import the certificate's associated secret into the same project where your Ingress resource for an app exists. If you want to use this certificate for apps in multiple projects, repeat this command for each project.<p class="note">Do not create the secret with the same name as the IBM-provided Ingress secret, which you can find by running `ibmcloud oc cluster get --cluster <cluster_name_or_ID> | grep Ingress`.</p>
  ```
  ibmcloud oc ingress secret create --name <secret_name> --cluster <cluster_name_or_ID> --cert-crn <certificate_crn> --namespace <project>
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

## Customizing the Ingress class
{: #ingress-class}



As of Kubernetes version 1.18, the new [`IngressClass` resource](https://kubernetes.io/docs/concepts/services-networking/ingress/#ingress-class){: external} replaces the deprecated `kubernetes.io/ingress.class` annotation.
{: shortdesc}

An `IngressClass` resource associates a class name with an Ingress controller type. Within the `IngressClass`, you can optionally set the class as the default Ingress class by including the `ingressclass.kubernetes.io/is-default-class: "true"` annotation. Then, in the Ingress resources that you create to define routing for your app service paths, you specify the class name in the `spec.ingressClassName` field to apply the Ingress resource to the Ingress controllers that are associated with that class.

Note that because the deprecated `kubernetes.io/ingress.class` annotation is still usable, classes that are specified in Ingress resources are applied in the following ways:
* If a class is specified either in the `spec.ingressClassName` field or in the deprecated `kubernetes.io/ingress.class` annotation, the class is applied.
* If both the `spec.ingressClassName` field and the `kubernetes.io/ingress.class` annotation and specified, the class in the annotation is used.
* If neither the `spec.ingressClassName` field nor the `kubernetes.io/ingress.class` annotation are specified, the default class is applied.


### Default Ingress classes for public and private ALBs
{: #ingress-class-default}

In {{site.data.keyword.containerlong_notm}} clusters that run Kubernetes version 1.18 or later and that are created on or after 01 December 2020, `IngressClass` resources are created by default for public and private ALBs.
{: shortdesc}

**Public ALBs**: The following `IngressClass` is automatically created in the `kube-system` namespace to configure all public ALBs in your cluster with the `public-iks-k8s-nginx` class. To apply an Ingress resource that you create to the public ALBs in your cluster, specify `ingressClassName: "public-iks-k8s-nginx"` in the `spec` section of your Ingress resource.

The `IngressClass` for public ALBs, `public-iks-k8s-nginx`, is set as the default class in your cluster. If you do not specify an `ingressClassName` field (or the deprecated `kubernetes.io/ingress.class` annotation) in your Ingress resource, the resource it applied to the public ALBs in your cluster.
{: note}

```yaml
apiVersion: networking.k8s.io/v1
kind: IngressClass
metadata:
  name: public-iks-k8s-nginx
  annotations:
    ingressclass.kubernetes.io/is-default-class: "true"
spec:
  controller: "k8s.io/ingress-nginx"
```
{: screen}

**Private ALBs**: The following `IngressClass` is automatically created in the `kube-system` namespace to configure all public ALBs in your cluster with the `private-iks-k8s-nginx` class. To apply an Ingress resource that you create to the public ALBs in your cluster, specify `ingressClassName: "private-iks-k8s-nginx"` in the `spec` section of your Ingress resource.

```yaml
apiVersion: networking.k8s.io/v1
kind: IngressClass
metadata:
  name: private-iks-k8s-nginx
spec:
  controller: "k8s.io/ingress-nginx"
```
{: screen}

The `public-iks-k8s-nginx` and `private-iks-k8s-nginx` `IngressClass` resources are not automatically created for existing 1.18 clusters that were created before 01 December 2020. In these clusters, you can still use the `kubernetes.io/ingress.class` annotation in your Ingress resources to specify `public-iks-k8s-nginx` or `private-iks-k8s-nginx` classes. However, to use the new Ingress class functionality, you can manually create these `IngressClass` resources in your cluster and specify the `ingressClassName` field in your Ingress resources.
{: important}

### Custom Ingress classes
{: #ingress-class-custom}

You can configure your own classes by creating custom `IngressClass` resources and changing the ALB deployment.
{: shortdesc}



1. Create an `IngressClass` resource. If you want this class to be the default class for your cluster, include the `ingressclass.kubernetes.io/is-default-class: "true"` annotation so that any Ingress resources that do not specify an Ingress class use this class by default.<p class="tip">For configurations in which another component manages your Ingress ALBs, such as if Ingress is deployed as part of a Helm chart, a class might already be created. In this case, you can continue to step 3.</p>
  ```yaml
  apiVersion: networking.k8s.io/v1
  kind: IngressClass
  metadata:
    name: <class_name>
    annotations:
      ingressclass.kubernetes.io/is-default-class: "true"
  spec:
    controller: "k8s.io/ingress-nginx"
  ```
  {: codeblock}

2. Deploy the `IngressClass` to your cluster.
  ```
  kubectl apply -f <class_name>.yaml -n <namespace>
  ```
  {: pre}

3. If you want the Kubernetes Ingress ALBs in your cluster to process Ingress resources of this class, [specify the custom class in an `ibm-ingress-deploy-config` configmap and update your ALBs to pick up the changes](/docs/openshift?topic=openshift-comm-ingress-annotations#comm-customize-deploy).

4. In your Ingress resources, specify the `ingressClassName: "<class_name>"` field in the `spec` section of your Ingress resource. Do not include the deprecated `kubernetes.io/ingress.class` annotation. Note that if you do not specify an Ingress class in an Ingress resource, then the default class is applied.

## Customizing routing and settings by using annotations and configmaps
{: #cm-annotations}

You can modify default ALB settings and add annotations to your Ingress resources.
{: shortdesc}

* To manage how requests are routed to your app, specify [Kubernetes NGINX annotations](/docs/openshift?topic=openshift-comm-ingress-annotations#annotations) (`nginx.ingress.kubernetes.io/<annotation>`) in your Ingress resources.
* To modify default Ingress settings, such as to enable source IP preservation or configure SSL protocols, [change the `ibm-cloud-provider-ingress-cm`, `ibm-k8s-controller-config`, or `ibm-ingress-deploy-config` configmap resources](/docs/openshift?topic=openshift-comm-ingress-annotations) for your Ingress ALBs.

## Updating ALBs
{: #alb-update}

Choose the image type and image version for your ALBs, and keep the image version for your ALB pods up to date.
{: shortdesc}

### Choosing a supported image version
{: #alb-version-choose}

<img src="images/icon-version-311.png" alt="Version 3.11 icon" width="30" style="width:30px; border-style: none"/> This information is for clusters that run {{site.data.keyword.openshiftshort}} version 3.11 only. To learn about Ingress for {{site.data.keyword.openshiftshort}} version 4, see [About Ingress in {{site.data.keyword.openshiftshort}} version 4 or later](/docs/openshift?topic=openshift-ingress-about-roks4).
{: important}

As of 01 December 2020, {{site.data.keyword.openshiftlong_notm}} primarily supports the Kubernetes Ingress image for the Ingress application load balancers (ALBs) in your cluster. The Kubernetes Ingress image is built on the community Kubernetes project's implementation of the NGINX Ingress controller. The previously supported {{site.data.keyword.openshiftlong_notm}} Ingress image, which was built on a custom implementation of the NGINX Ingress controller, is deprecated.
{: shortdesc}

**Clusters created on or after 01 December 2020**: Default application load balancers (ALBs) run the Kubernetes Ingress image in all new {{site.data.keyword.openshiftlong_notm}} clusters that run version 3.11.

**Clusters created before 01 December 2020**:
* Existing clusters with ALBs that run the custom IBM Ingress image continue to operate as-is.
* Support for the custom IBM Ingress image ends in 6 months on 30 April 2021.
* You must move to the new Kubernetes Ingress by migrating any existing Ingress setups. Your existing ALBs and other Ingress resources are not automatically migrated to the new Kubernetes Ingress image.
* You can easily migrate to Kubernetes Ingress by using the [migration tool](/docs/openshift?topic=openshift-ingress-types#alb-type-migration) that is developed and supported by IBM Cloud Kubernetes Service.
* If you do not move to Kubernetes Ingress before 30 April 2020, ALBs that run the custom IBM Ingress image continue to run, but all support from IBM Cloud for those ALBs is discontinued.

You can manage the versions of your ALBs in the following ways:
* When you create a new ALB, enable an ALB that was previously disabled, or manually update an ALB, you can specify an image version for your ALB in the `--version` flag.
* To specify a version other than the default, you must first disable automatic updates by running the `ibmcloud oc ingress alb autoupdate disable` command.
* If you omit the `--version` flag when you enable or update an existing ALB, the ALB runs the default version of the same image that the ALB previously ran: either the Kubernetes Ingress image or the {{site.data.keyword.openshiftlong_notm}} Ingress image.

To list the latest three versions that are supported for each type of image, run the following command:
```
ibmcloud oc ingress alb versions
```
{: pre}

Example output:
```
IBM Cloud Ingress: 'auth' version
425

IBM Cloud Ingress versions
653 (default)
652
651

Kubernetes Ingress versions
0.35.0_474_iks
0.34.1_391_iks (default)
0.33.0_390_iks
```
{: screen}

The Kubernetes Ingress version follows the format `<community_version>_<ibm_build>_iks`. The IBM build number indicates the most recent build of the Kubernetes Ingress NGINX release that {{site.data.keyword.openshiftlong_notm}} released. For example, the version `0.35.0_474_iks` indicates the most recent build of the `0.35.0` Ingress NGINX version. {{site.data.keyword.openshiftlong_notm}} might release builds of the community image version to address vulnerabilities.

For the changes that are included in each version of the Ingress images, see the [Ingress version changelog](/docs/containers?topic=containers-cluster-add-ons-changelog).

### Managing automatic updates
{: #autoupdate}

Manage automatic updates of all Ingress ALB pods in a cluster.
{: shortdesc}

By default, automatic updates to Ingress ALBs are enabled. ALB pods are automatically updated by IBM when a new image version is available. If your ALBs run the Kubernetes Ingress image, your ALBs are automatically updated to the latest version of the Kubernetes Ingress NGINX image. For example, if your ALBs run version `0.34.1_391_iks`, and the Kubernetes Ingress NGINX image `0.35.0` is released, your ALBs are automatically updated to the latest build of the latest community version, such as `0.35.0_474_iks`.

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

If automatic updates for the Ingress ALB add-on are disabled and you want to update the add-on, you can force a one-time update of your ALB pods. Note that you can use this command to update your ALB image to a different version, but you cannot use this command to change your ALB from one type of image to another. Your ALB continues to run the image that it previously ran: either the Kubernetes Ingress image or the {{site.data.keyword.openshiftlong_notm}} Ingress image. After you force a one-time update, automatic updates remain disabled.
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

The image version that you change your ALB to must be a supported image version that is listed in the output of `ibmcloud oc ingress alb versions`. Note that you can use this command to change your ALB image to a different version, but you cannot use this command to change your ALB from one type of image to another. After you force a one-time update, automatic updates to your ALBs are disabled.

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
  private-crdf253b6025d64944ab99ed63bb4567b6-alb1   false     disabled   private   -               dal12   ingress:653/ingress-auth:425   2294021       -
  private-crdf253b6025d64944ab99ed63bb4567b6-alb2   false     disabled   private   -               dal10   ingress:653/ingress-auth:425   2234947       -
  public-crdf253b6025d64944ab99ed63bb4567b6-alb1    true      enabled    public    169.48.228.78   dal12   ingress:653/ingress-auth:425   2294019       -
  public-crdf253b6025d64944ab99ed63bb4567b6-alb2    true      enabled    public    169.46.17.6     dal10   ingress:653/ingress-auth:425   2234945       -
  public-crdf253b6025d64944ab99ed63bb4567b6-alb3    true      enabled    public    169.49.28.09    dal12   ingress:653/ingress-auth:425   2294019       -
  public-crdf253b6025d64944ab99ed63bb4567b6-alb4    true      enabled    public    169.50.35.62    dal10   ingress:653/ingress-auth:425   2234945       -
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
    private-crdf253b6025d64944ab99ed63bb4567b6-alb1   false     disabled   private   -               dal12   ingress:653/ingress-auth:425   2294021
    private-crdf253b6025d64944ab99ed63bb4567b6-alb2   false     disabled   private   -               dal10   ingress:653/ingress-auth:425   2234947
    public-crdf253b6025d64944ab99ed63bb4567b6-alb1    true      enabled    public    169.48.228.78   dal12   ingress:653/ingress-auth:425   2294019
    public-crdf253b6025d64944ab99ed63bb4567b6-alb2    true      enabled    public    169.46.17.6     dal10   ingress:653/ingress-auth:425   2234945
    public-crdf253b6025d64944ab99ed63bb4567b6-alb3    true      enabled    public    169.49.28.09    dal12   ingress:653/ingress-auth:425   2294030
    public-crdf253b6025d64944ab99ed63bb4567b6-alb4    true      enabled    public    169.50.35.62    dal10   ingress:653/ingress-auth:425   2234940
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
    private-crdf253b6025d64944ab99ed63bb4567b6-alb1   false     disabled   private   -               dal12   ingress:653/ingress-auth:425   2294021
    private-crdf253b6025d64944ab99ed63bb4567b6-alb2   false     disabled   private   -               dal10   ingress:653/ingress-auth:425   2234947
    public-crdf253b6025d64944ab99ed63bb4567b6-alb1    false     disabled   public    169.48.228.78   dal12   ingress:653/ingress-auth:425   2294019
    public-crdf253b6025d64944ab99ed63bb4567b6-alb2    false     disabled   public    169.46.17.6     dal10   ingress:653/ingress-auth:425   2234945
    public-crdf253b6025d64944ab99ed63bb4567b6-alb3    true      enabled    public    169.49.28.09    dal12   ingress:653/ingress-auth:425   2294030
    public-crdf253b6025d64944ab99ed63bb4567b6-alb4    true      enabled    public    169.50.35.62    dal10   ingress:653/ingress-auth:425   2234940
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

