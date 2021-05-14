---

copyright:
  years: 2014, 2021
lastupdated: "2021-05-14"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift
content-type: troubleshoot

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
 

# Version 4: Why does the VPC load balancer for router only route to one zone?
{: #router-mzr-error}

**Supported infrastructure provider and versions**:
* <img src="../../images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC
* <img src="../../images/icon-version-43.png" alt="Version 4 icon" width="30" style="width:30px; border-style: none"/> {{site.data.keyword.openshiftshort}} version 4 clusters

{: tsSymptoms}
You create a multizone VPC cluster. However, when you run `ibmcloud is load-balancers` to find the VPC load balancer that exposes the router, the VPC subnet for only one zone in your cluster is listed instead of the subnets for all zones in your cluster. In the output, look for the VPC load balancer **Name** that starts with `kube-crtmgr-<cluster_ID>`.
```
ID                                          Name                                                         Family        Subnets               Is public   Provision status   Operating status   Resource group
r006-d044af9b-92bf-4047-8f77-a7b86efcb923   kube-bsaucubd07dhl66e4tgg-1f4f408ce6d2485499bcbdec0fa2d306   Application   mysubnet-us-south-3   true        active             online             default
```
{: screen}


{: tsCauses}
When you create an {{site.data.keyword.openshiftlong_notm}} cluster on VPC infrastructure in the CLI, the cluster is initially created with worker nodes in one zone only. You then make the cluster multizone by manually adding zones to your worker pools with the `ibmcloud oc zone add vpc-gen2` command. Currently, when you add zones to your cluster, the Ingress controller is not updated with the VPC subnets for the new zones, and does not route requests to apps in the new zones.

{: tsResolve}
Restart the Ingress controller so that a new VPC load balancer is created, which registers the router behind a hostname and forwards traffic to the router. Then, update your Ingress subdomain to use the new VPC load balancer hostname.

1. Delete the `default` Ingress controller. After, the Ingress controller is automatically re-created.
  ```
  oc delete ingresscontroller default -n openshift-ingress-operator
  ```
  {: pre}

2. Verify that the `default` Ingress controller is re-created.
  ```
  oc get ingresscontroller -n openshift-ingress-operator
  ```
  {: pre}

  Example output:
  ```
  NAME      AGE
  default   2m38s
  ```
  {: screen}

3. Verify that the new VPC load balancer that exposes the router has **Provision status** of `active` and an **Operating status** of `online`. Also, verify that the **Subnets** list now includes subnets for each zone of your cluster.
  ```
  ibmcloud is load-balancers
  ```
  {: pre}

  In the output, look for the VPC load balancer **Name** that starts with `kube-crtmgr-<cluster_ID>`.
  ```
  ID                                          Name                                                         Family        Subnets               Is public   Provision status   Operating status   Resource group
  r006-d044af9b-92bf-4047-8f77-a7b86efcb923   kube-bsaucubd07dhl66e4tgg-1f4f408ce6d2485499bcbdec0fa2d306   Application   mysubnet-us-south-1, mysubnet-us-south-2, mysubnet-us-south-3   true        active             online             default
  ```
  {: screen}

4. For the `router-default` service, copy the hostname that is assigned by the new VPC load balancer in the **EXTERNAL-IP** field.
  ```
  oc get svc -n openshift-ingress
  ```
  {: pre}

  Example output:
  ```
  NAME                       TYPE           CLUSTER-IP      EXTERNAL-IP                            PORT(S)                      AGE
  router-default             LoadBalancer   172.21.47.119   1234abcd-us-south.lb.appdomain.cloud   80:32637/TCP,443:31719/TCP   2m
  router-internal-default    ClusterIP      172.21.51.30    <none>                                 80/TCP,443/TCP,1936/TCP      2m
  ```
  {: screen}

5. Get the Ingress subdomain for your cluster.
  ```
  ibmcloud oc cluster get -c <cluster_name_or_ID> | grep 'Ingress Subdomain'
  ```
  {: pre}

  Example output:
  ```
  Ingress Subdomain:              mycluster-35366fb2d3d90fd50548180f69e7d12a-0000.us-south.containers.appdomain.cloud
  ```
  {: screen}

6. Update the Ingress subdomain DNS registration to use the new VPC load balancer hostname.
  ```
  ibmcloud oc nlb-dns replace --cluster <cluster_name_or_ID> --nlb-subdomain <Ingress_subdomain> --lb-host <vpc_lb_hostname>
  ```
  {: pre}

7. Verify that the ingress subdomain DNS registration is updated to include the new VPC load balancer hostname for your router.
  ```
  ibmcloud oc nlb-dns ls -c <cluster_name_or_ID>
  ```
  {: pre}

  Example output:
  ```
  Subdomain                                                                             Load Balancer Hostname                 SSL Cert Status   SSL Cert Secret Name                            Secret Namespace   
  mycluster-d84d4d2137685d8446c88eacf59b5038-0000.us-south.containers.appdomain.cloud   1234abcd-us-south.lb.appdomain.cloud   created           cluster-d84d4d2137685d8446c88eacf59b5038-0000   openshift-ingress
  ```
  {: screen}


