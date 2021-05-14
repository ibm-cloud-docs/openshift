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
 

# VPC clusters: Why does a Kubernetes `LoadBalancer` service fail with no IPs?
{: #vpc_no_lb}

**Infrastructure provider**: <img src="../../images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC

{: tsSymptoms}
<img src="../../images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> You publicly exposed your app by creating a Kubernetes `LoadBalancer` service in your VPC cluster. When you run `oc describe svc <kubernetes_lb_service_name>`, you see a warning message in the **Events** section similar to one of the following:
```
The subnet with ID(s) '<subnet_id>' has insufficient available ipv4 addresses.
```
{: screen}

{: tsCauses}
When you create a Kubernetes `LoadBalancer` service in your cluster, a VPC load balancer is automatically created in your VPC. The VPC load balancer puts a floating IP address for your Kubernetes `LoadBalancer` service behind a hostname that you can access your app through.

In VPC clusters, both worker nodes and services are assigned IP addresses from the same subnets. Traffic routing is enabled between subnets, so when all IP addresses in a subnet for a zone are used by worker nodes or services, you can still create new worker nodes or services in that zone because they use IP addresses from subnets in other zones. However, if all IP addresses on all subnets are in use, a new Kubernetes `LoadBalancer` service cannot be successfully provisioned.

{: tsResolve}
After you create a VPC subnet, you cannot resize it or change its IP range. Instead, you must create a larger VPC subnet in one or more zones where you have worker nodes. Then you create a new worker pool using the larger subnets.

1. [Create a new VPC subnet](https://cloud.ibm.com/vpc/provision/network){: external} in the same VPC and in one or more zones where your cluster has worker nodes. Make sure that you create a subnet that can support both the number of worker nodes and services that you plan to create in your cluster. The default CIDR size of each VPC subnet is `/24`, which can support up to 253 worker nodes and services. To check your cluster's VPC and zones, run `ibmcloud oc cluster get --cluster <cluster_name_or_ID>`.

2. Create a new worker pool in your cluster.
   ```
   ibmcloud oc worker-pool create vpc-gen2 --name <name> --cluster <cluster_name_or_ID> --flavor <flavor> --size-per-zone <number_of_worker_nodes> --label <key>=<value>
   ```
   {: pre}

3. Using the ID for the larger subnets that you created in step 1, add the zones to the worker pool. Repeat the following command for each zone and subnet.
    ```
    ibmcloud oc zone add vpc-gen2 --zone <zone> --subnet-id <subnet_id> --cluster <cluster_name_or_ID> --worker-pool <worker_pool_name>
    ```
    {: pre}

4. After a few minutes, verify that your `LoadBalancer` service is successfully provisioned onto one of the new subnets. If the service is provisioned successfully, no `Warning` or `Error` events are displayed.
  ```
  oc describe svc <kubernetes_lb_service_name>
  ```
  {: pre}
