---

copyright:
  years: 2014, 2020
lastupdated: "2020-12-01"

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



# About Ingress in {{site.data.keyword.openshiftshort}} 3.11
{: #ingress-about}

<img src="images/icon-version-311.png" alt="Version 3.11 icon" width="30" style="width:30px; border-style: none"/> This information is for clusters that run {{site.data.keyword.openshiftshort}} version 3.11 only. To learn about Ingress for {{site.data.keyword.openshiftshort}} version 4, see [About Ingress in {{site.data.keyword.openshiftshort}} version 4](/docs/openshift?topic=openshift-ingress-about-roks4).
{: important}

Ingress is a Kubernetes service that balances network traffic workloads in your cluster by forwarding public or private requests to your apps. You can use Ingress to expose multiple app services to the public or to a private network by using a unique public or private route.
{: shortdesc}

The Ingress application load balancer (ALB) is a layer 7 load balancer which implements the NGINX Ingress controller. A layer 4 `LoadBalancer` service exposes the ALB so that the ALB can receive external requests that come into your cluster. The ALB then routes requests to app pods in your cluster based on distinguishing layer 7 protocol characteristics, such as headers.

## What are the components of Ingress?
{: #ingress_components}

Ingress consists of three components:
*   Ingress resources
*   Application load balancers (ALBs)
*   A multizone load balancer (MZLB).
{: shortdesc}

### Ingress resource
{: #ingress-resource}

To expose an app by using Ingress, you must create a Kubernetes service for your app and register this service with Ingress by defining an Ingress resource. The Ingress resource is a Kubernetes resource that defines the rules for how to route incoming requests for apps.
{: shortdesc}

The Ingress resource also specifies the path to your app services. When you create a standard cluster, an Ingress subdomain is registered by default for your cluster in the format `<cluster_name>.<globally_unique_account_HASH>-0000.<region>.containers.appdomain.cloud`. The paths to your app services are appended to the public route to form a unique app URL such as `mycluster-a1b2cdef345678g9hi012j3kl4567890-0000.us-south.containers.appdomain.cloud/myapp1`. The following table describes each component of the subdomain.

|Subdomain component|Description|
|----|----|
|`*`|The wildcard for the subdomain is registered by default for your cluster.|
|`<cluster_name>`|The name of your cluster.<ul><li>If the cluster name is 26 characters or fewer and the cluster name is unique in this region, the entire cluster name is included and is not modified: `myclustername`.</li><li>If the cluster name is 26 characters or fewer and there is an existing cluster of the same name in this region, the entire cluster name is included and a dash with six random characters is added: `myclustername-ABC123`.</li><li>If the cluster name is 26 characters or greater and the cluster name is unique in this region, only the first 24 characters of the cluster name are used: `myveryverylongclusternam`.</li><li>If the cluster name is 26 characters or greater and there is an existing cluster of the same name in this region, only the first 17 characters of the cluster name are used and a dash with six random characters is added: `myveryverylongclu-ABC123`.</li></ul>|
|`<globally_unique_account_HASH>`|A globally unique HASH is created for your {{site.data.keyword.cloud_notm}} account. All subdomains that you create for NLBs in clusters in your account use this globally unique HASH.|
|`0000`|The first and second characters indicate a public or a private (internal) subdomain. `00` indicates a subdomain that has a public DNS entry. `i0` indicates a subdomain that has a private DNS entry. The third and fourth characters, such as `00` or another number, act as a counter for each subdomain that is created in your cluster.|
|`<region>`|The region that the cluster is created in.|
|`containers.appdomain.cloud`|The subdomain for {{site.data.keyword.openshiftlong_notm}} subdomains.|
{: caption="Understanding the Ingress subdomain format"}

One Ingress resource is required per project where you have apps that you want to expose.
* If the apps in your cluster are all in the same namespace, one Ingress resource is required to define routing rules for the apps that are exposed there. Note that if you want to use different domains for the apps within the same namespace, you can use a wildcard domain to specify multiple subdomain hosts within one resource.
* If the apps in your cluster are in different namespaces, you must create one resource per project to define rules for the apps that are exposed there. You must use a wildcard domain and specify a different subdomain in each Ingress resource.

### Application load balancer (ALB)
{: #alb-about}

The application load balancer (ALB) is an external load balancer that listens for incoming HTTP, HTTPS, or TCP service requests. The ALB then forwards requests to the appropriate app pod according to the rules defined in the Ingress resource.
{: shortdesc}

When you create a standard cluster, {{site.data.keyword.openshiftlong_notm}} automatically creates a highly available ALB in each zone where you have worker nodes and assigns a unique public domain which all public ALBs share. You can find the public domain for your cluster by running `ibmcloud oc cluster get --cluster <cluster_name_or_ID>` and looking for the **Ingress subdomain** in the format `mycluster-<hash>0001.us-south.containers.appdomain.cloud`. One default private ALB is also automatically created in each zone of your cluster, but the private ALBs are not automatically enabled and do not use the Ingress subdomain. Note that clusters with workers that are connected to private VLANs only are not assigned an IBM-provided Ingress subdomain.

In classic clusters, the Ingress subdomain for your cluster is linked to the public ALB IP addresses. You can find the IP address of each public ALB by running `ibmcloud oc ingress alb ls --cluster <cluster_name_or_ID>` and looking for the **ALB IP** field. The portable public and private ALB IP addresses are provisioned into your IBM Cloud infrastructure account during cluster creation and are static floating IPs that do not change for the life of the cluster. If the worker node is removed, Kubernetes deployment manager reschedules the ALB pods that were on that worker to another worker node in that zone. The rescheduled ALB pods retain the same static IP address. However, if you remove a zone from a cluster, then the ALB IP address for that zone is removed.

Do not delete the services that expose your ALBs on public or private IP addresses. These services are formatted such as `public-crdf253b6025d64944ab99ed63bb4567b6-alb1`.
{: note}

### Multizone load balancer (MZLB)
{: #mzlb}

A Cloudflare multizone load balancer (MZLB) health checks your ALBs.
{: shortdesc}

Whenever you create a multizone cluster or [add a zone to a single zone cluster](/docs/openshift?topic=openshift-add_workers#add_zone), a Cloudflare multizone load balancer (MZLB) is automatically created and deployed so that 1 MZLB exists for each region. The MZLB puts the IP addresses of your ALBs behind the same subdomain and enables health checks on these IP addresses to determine whether they are available or not.

For example, if your cluster has worker nodes in 3 zones in the US-East region, the subdomain `mycluster-a1b2cdef345678g9hi012j3kl4567890-0000.us-east.containers.appdomain.cloud` has 3 ALB IP addresses. The MZLB health checks the public ALB IP in each zone of a region and keeps the DNS lookup results updated based on these health checks. For example, if your ALBs have IP addresses `1.1.1.1`, `2.2.2.2`, and `3.3.3.3`, a normal operation DNS lookup of your Ingress subdomain returns all 3 IPs, 1 of which the client accesses at random. If the ALB with IP address `3.3.3.3` becomes unavailable for any reason, such as due to zone failure, then the health check for that zone fails, the MZLB removes the failed IP from the subdomain, and the DNS lookup returns only the healthy `1.1.1.1` and `2.2.2.2` ALB IPs. The subdomain has a 30 second time to live (TTL), so after 30 seconds, new client apps can access only one of the available, healthy ALB IPs.

In rare cases, some DNS resolvers or client apps might continue to use the unhealthy ALB IP after the 30-second TTL. These client apps might experience a longer load time until the client app abandons the `3.3.3.3` IP and tries to connect to `1.1.1.1` or `2.2.2.2`. Depending on the client browser or client app settings, the delay can range from a few seconds to a full TCP timeout.

Because Cloudflare is a public service, the MZLB load balances for public ALBs that use the IBM-provided Ingress subdomain only. If you use only private ALBs, you must manually check the health of the ALBs and update DNS lookup results. If you use public ALBs that use a custom domain, you can include the ALBs in MZLB load balancing by creating a CNAME in your DNS entry to forward requests from your custom domain to the IBM-provided Ingress subdomain for your cluster.

If you use Calico pre-DNAT network policies to block all incoming traffic to Ingress services, you must allow inbound access on port 80 to your ALBs from [the IP addresses in step 6 of this section](/docs/openshift?topic=openshift-firewall#iam_allowlist) and [Cloudflare's IPv4 IP addresses](https://www.cloudflare.com/ips/){: external} so that the {{site.data.keyword.openshiftshort}} control plane can check the health of your routers. For steps on how to create a Calico pre-DNAT policy to allow these IP addresses, see [Lesson 3 of the Calico network policy tutorial](/docs/containers?topic=containers-policy_tutorial#lesson3).
{: note}

<br />

## How does a request get to my app?
{: #architecture-classic}

### Single-zone cluster
{: #classic-single}

<img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> The following diagram shows how Ingress directs communication from the internet to an app in a classic single-zone cluster.
{: shortdesc}

<img src="images/cs_ingress_singlezone.png" width="600" alt="Expose an app in a single-zone cluster by using Ingress" style="width:600px; border-style: none"/>

1. A user sends a request to your app by accessing your app's URL. This URL is the Ingress subdomain for your cluster appended with the Ingress resource path for your exposed app, such as `mycluster-<hash>-0000.us-south.containers.appdomain.cloud/myapp`.

2. A DNS system service resolves the subdomain in the URL to the portable public IP address of the load balancer that exposes the ALB in your cluster.

3. Based on the resolved IP address, the client sends the request to the Kubernetes load balancer service that exposes the ALB.

4. The load balancer service routes the request to the ALB.

5. The ALB checks if a routing rule for the `myapp` path in the cluster exists. If a matching rule is found, the request is proxied according to the rules that you defined in the Ingress resource to the pod where the app is deployed. The source IP address of the package is changed to the IP address of the worker node where the app pod runs. If multiple app instances are deployed in the cluster, the ALB load balances the requests between the app pods.

6. When the app returns a response packet, it uses the IP address of the worker node where the ALB that forwarded the client request exists. The ALB then sends the response packet to the client.

### Multizone cluster
{: #classic-multi}

<img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> The following diagram shows how Ingress directs communication from the internet to an app in a classic multizone cluster.
{: shortdesc}

<img src="images/cs_ingress_multizone.png" width="800" alt="Expose an app in a multizone cluster by using Ingress" style="width:800px; border-style: none"/>

1. A user sends a request to your app by accessing your app's URL. This URL is the Ingress subdomain for your cluster appended with the Ingress resource path for your exposed app, such as `mycluster-<hash>-0000.us-south.containers.appdomain.cloud/myapp`.

2. A DNS system service, which acts as the global load balancer, resolves the subdomain in the URL to an available IP address that was reported as healthy by the MZLB. The MZLB continuously checks the portable public IP addresses of the load balancer services that expose public ALBs in each zone in your cluster. The IP addresses are resolved in a round-robin cycle, ensuring that requests are equally load balanced among the healthy ALBs in various zones.

3. The client sends the request to the IP address of the Kubernetes load balancer service that exposes an ALB.

4. The load balancer service routes the request to the ALB.

5. The ALB checks if a routing rule for the `myapp` path in the cluster exists. If a matching rule is found, the request is proxied according to the rules that you defined in the Ingress resource to the pod where the app is deployed. The source IP address of the package is changed to the public IP address of the worker node where the app pod runs. If multiple app instances are deployed in the cluster, the ALB load balances the requests between app pods across all zones.

6. When the app returns a response packet, it uses the IP address of the worker node where the ALB that forwarded the client request exists. The ALB then sends the response packet to the client.

<br />

## Do I use the {{site.data.keyword.openshiftlong_notm}} Ingress image or the Kubernetes Ingress image?
{: #choose_images}

<img src="images/icon-version-311.png" alt="Version 3.11 icon" width="30" style="width:30px; border-style: none"/> This information is for clusters that run {{site.data.keyword.openshiftshort}} version 3.11 only. To learn about Ingress for {{site.data.keyword.openshiftshort}} version 4, see [About Ingress in {{site.data.keyword.openshiftshort}} version 4 or later](/docs/openshift?topic=openshift-ingress-about-roks4).
{: important}

As of 01 December 2020, {{site.data.keyword.openshiftlong_notm}} primarily supports the Kubernetes Ingress image for the Ingress application load balancers (ALBs) in your cluster. The Kubernetes Ingress image is built on the community Kubernetes project's implementation of the NGINX Ingress controller. The previously supported {{site.data.keyword.openshiftlong_notm}} Ingress image, which was built on a custom implementation of the NGINX Ingress controller, is deprecated.
{: shortdesc}

**Clusters created on or after 01 December 2020**: Default application load balancers (ALBs) run the Kubernetes Ingress image in all new {{site.data.keyword.openshiftlong_notm}} clusters that run version 3.11.

**Clusters created before 01 December 2020**:
* Existing clusters with ALBs that run the custom IBM Ingress image continue to operate as-is.
* Support for the custom IBM Ingress image ends in 6 months on 30 April 2021.
* You must move to the new Kubernetes Ingress by migrating any existing Ingress setups. Your existing ALBs and other Ingress resources are not automatically migrated to the new Kubernetes Ingress image.
* You can easily migrate to Kubernetes Ingress by using the [migration tool](#alb-type-migration) that is developed and supported by IBM Cloud Kubernetes Service.
* If you do not move to Kubernetes Ingress before 30 April 2020, ALBs that run the custom IBM Ingress image continue to run, but all support from IBM Cloud for those ALBs is discontinued.

To get started, see [Setting up Kubernetes Ingress](/docs/openshift?topic=openshift-ingress-types).

Not ready to switch your ALBs to the Kubernetes Ingress image yet? When you enable or update an existing ALB, the ALB continues to run the same image that the ALB previously ran: either the Kubernetes Ingress image or the {{site.data.keyword.openshiftlong_notm}} Ingress image. Your existing ALBs do not begin to run the Kubernetes Ingress image until you specify the Kubernetes Ingress image version in the `--version` flag when you enable them.
{: tip}

For a comparison of the Kubernetes Ingress image and the deprecated IBM Ingress image, review the following tables.

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

## How can I enable TLS certificates?
{: #enable-certs}

To load balance incoming HTTPS connections to your subdomain, you can configure the ALB to decrypt the network traffic and forward the decrypted request to the apps that are exposed in your cluster.
{: shortdesc}

When you configure the public ALB, you choose the domain that your apps are accessible through. If you use the IBM-provided domain, such as `mycluster-<hash>-0000.us-south.containers.appdomain.cloud/myapp`, you can use the default TLS certificate that is created for the Ingress subdomain. If you set up a CNAME record to map a custom domain to the IBM-provided domain, you can provide your own TLS certificate for your custom domain.

TLS secret configuration depends on the type of Ingress controller image that your ALB runs. For information about how to manage TLS certificates and secrets for Ingress, see the [Kubernetes Ingress image TLS documentation](/docs/openshift?topic=openshift-ingress-types#manage_certs) or [{{site.data.keyword.openshiftlong_notm}} Ingress image TLS documentation](/docs/openshift?topic=openshift-ingress#manage_certs).

<br />

## How can I customize routing?
{: #custom-routing}

You can modify default ALB settings and add annotations to your Ingress resources.
{: shortdesc}

Depending on which image type you choose, the ALB behaves according to that implementation of the NGINX Ingress controller.

**ALBs that run the Kubernetes image (default)**:
* To manage how requests are routed to your app, specify [Kubernetes NGINX annotations](/docs/openshift?topic=openshift-comm-ingress-annotations#annotations) (`nginx.ingress.kubernetes.io/<annotation>`) in your Ingress resources.
* To modify default Ingress settings, such as to enable source IP preservation or configure SSL protocols, [change the `ibm-cloud-provider-ingress-cm`, `ibm-k8s-controller-config`, or `ibm-ingress-deploy-config` configmap resources](/docs/openshift?topic=openshift-ingress_annotation) for your Ingress ALBs.

**ALBs that run the custom {{site.data.keyword.openshiftlong_notm}} image**:
* To manage how requests are routed to your app, specify [custom {{site.data.keyword.openshiftlong_notm}} annotations](/docs/openshift?topic=openshift-ingress_annotation) (`ingress.bluemix.net/<annotation>`) in your Ingress resources.
* To modify default Ingress settings, such as to enable source IP preservation or configure SSL protocols, [change the `ibm-cloud-provider-ingress-cm` configmap resource](/docs/openshift?topic=openshift-ingress_annotation#preserve_source_ip) for your Ingress ALBs.

<br />

## How do I manage the lifecycle of my ALBs?
{: #alb-lifecycle}

Ingress ALBs are managed by {{site.data.keyword.openshiftlong_notm}}. To further modify and manage your ALBs, such as to manage version updates for your ALBs or to scale up ALB replicas, you can use `ibmcloud oc ingress alb` commands. For more information, see [Updating ALBs](/docs/containers?topic=containers-ingress#alb-update).
{: shortdesc}


