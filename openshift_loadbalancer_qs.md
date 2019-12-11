---

copyright:
  years: 2014, 2019
lastupdated: "2019-12-11"

keywords: openshift, roks, rhoks, rhos, nlb, lbaas

subcollection: containers

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:preview: .preview}

# Quick start for load balancers
{: #loadbalancer-qs}

Quickly expose your app to the Internet by creating a layer 4 load balancer.
{: shortdesc}

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
* [About network load balancers (NLBs)](/docs/openshift?topic=openshift-loadbalancer-about)
* [Setting up basic load balancing with an NLB 1.0](/docs/openshift?topic=openshift-loadbalancer)
* [Registering a DNS subdomain for an NLB](/docs/openshift?topic=openshift-loadbalancer_hostname)

