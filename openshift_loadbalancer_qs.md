---

copyright:
  years: 2014, 2020
lastupdated: "2020-07-31"

keywords: openshift, roks, rhoks, rhos, nlb, lbaas

subcollection: openshift

---

{:beta: .beta}
{:codeblock: .codeblock}
{:deprecated: .deprecated}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:gif: data-image-type='gif'}
{:help: data-hd-content-type='help'}
{:important: .important}
{:new_window: target="_blank"}
{:note: .note}
{:pre: .pre}
{:preview: .preview}
{:screen: .screen}
{:shortdesc: .shortdesc}
{:support: data-reuse='support'}
{:table: .aria-labeledby="caption"}
{:tip: .tip}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:step: data-tutorial-type='step'}


# Quick start for load balancers
{: #loadbalancer-qs}

Quickly expose your app to the Internet by creating a layer 4 load balancer.
{: shortdesc}

First time setting up a load balancer? Check out [Classic: Setting up basic load balancing with an NLB 1.0](/docs/openshift?topic=openshift-loadbalancer) or [VPC: Exposing apps with VPC load balancers](/docs/openshift?topic=openshift-vpc-lbaas) for prerequisite steps and more details. Come back to these quick start steps for a brief refresher the next time you set up a load balancer.
{: tip}


## Exposing an app by using an NLB in a classic cluster
{: #lb_qs_classic}

1. Expose your app by creating a version 1.0 network load balancer (NLB 1.0).
  ```
  oc expose deploy my-app --port=80 --target-port=8080 --type=LoadBalancer --name my-lb-svc
  ```
  {: pre}

2. Get the NLB 1.0 **EXTERNAL-IP** address.
  ```
  oc get svc my-lb-svc
  ```
  {: pre}

  Example output:
  ```
  NAME        TYPE           CLUSTER-IP      EXTERNAL-IP     PORT(S)        AGE
  my-lb-svc   LoadBalancer   172.XX.XXX.XX   169.XX.XXX.XX   80:31224/TCP   23s
  ```
  {: screen}

3. Curl your app's IP address.
  ```
  curl <external-ip>
  ```
  {: pre}

4. Optional: Create a hostname for your app.
  ```
  ibmcloud oc nlb-dns create classic -c <cluster_name_or_id> --ip <NLB_IP>
  ```
  {: pre}

  In a web browser, enter the hostname that is created. Example output:
  ```
  NLB hostname was created as mycluster-35366fb2d3d90fd50548180f69e7d12a-0001.us-south.containers.appdomain.cloud
  ```
  {: screen}

For more information, see:
* [Classic: About network load balancers (NLBs)](/docs/openshift?topic=openshift-loadbalancer-about)
* [Classic: Setting up basic load balancing with an NLB 1.0](/docs/openshift?topic=openshift-loadbalancer)
* [Classic: Setting up DSR load balancing with an NLB 2.0 (beta)](/docs/openshift?topic=openshift-loadbalancer-v2)
* [Classic: Registering a DNS subdomain for an NLB](/docs/openshift?topic=openshift-loadbalancer_hostname)

## Exposing an app by using a VPC load balancer in a VPC cluster
{: #lb_qs_vpc}

1. Expose your app by creating a Kubernetes `LoadBalancer` service.
  ```
  oc expose deploy my-app --port=80 --target-port=8080 --type=LoadBalancer --name my-lb-svc
  ```
  {: pre}

2. Get the service's hostname that is listed in the **EXTERNAL-IP** column. The VPC load balancer that assigns the hostname takes a few minutes to provision in your VPC. You cannot access your app by using the hostname of your Kubernetes `LoadBalancer` service until the VPC load balancer is fully provisioned.
  ```
  oc get svc my-lb-svc
  ```
  {: pre}

  Example output:
  ```
  NAME        TYPE           CLUSTER-IP      EXTERNAL-IP                            PORT(S)        AGE
  my-lb-svc   LoadBalancer   172.XX.XXX.XX   1234abcd-us-south.lb.appdomain.cloud   80:31224/TCP   23s
  ```
  {: screen}

3. In a web browser, enter the hostname that is created.

For more information, see [VPC: Exposing apps with VPC load balancers](/docs/openshift?topic=openshift-vpc-lbaas).

