---

copyright:
  years: 2014, 2019
lastupdated: "2019-07-23"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:note: .note}
{:download: .download}
{:preview: .preview}
{:faq: data-hd-content-type='faq'}


# FAQs
{: #faqs}

Review frequently asked questions for using {{site.data.keyword.openshiftlong}}.
{: shortdesc}

## What container platforms are available for my cluster?
{: #container_platforms}
{: faq}

With {{site.data.keyword.containerlong_notm}}, you can select from two container management platforms: the IBM version of community Kubernetes and Red Hat OpenShift on IBM Cloud (beta). The container platform that you select is installed on your cluster master and worker nodes. Later, you can [update the version](/docs/containers?topic=containers-update#update) but cannot roll back to a previous version or switch to a different container platform. If you want to use multiple container platforms, create a separate cluster for each. 

For more information, see [Comparison between OpenShift and community Kubernetes clusters](/docs/openshift?topic=openshift-why_openshift#openshift_kubernetes).

<dl>
  <dt>Kubernetes</dt>
    <dd>[Kubernetes ![External link icon](../icons/launch-glyph.svg "External link icon")](https://kubernetes.io/) is a production-grade, open source container orchestration platform that you can use to automate, scale, and manage your containerized apps that run on an Ubuntu operating system. With the [{{site.data.keyword.containerlong_notm}} version](/docs/containers?topic=containers-cs_versions#cs_versions), you get access to community Kubernetes API features that are considered **beta** or higher by the community. Kubernetes **alpha** features, which are subject to change, are generally not enabled by default. With Kubernetes, you can combine a variety of resources such as secrets, deployments, and services to securely create and manage highly available, containerized apps.<br><br>
    To get started, [create a Kubernetes cluster](/docs/containers?topic=containers-cs_cluster_tutorial#cs_cluster_tutorial).</dd>
  <dt>OpenShift</dt>
    <dd>Red Hat OpenShift on IBM Cloud is a Kubernetes-based platform that is designed especially to accelerate your containerized app delivery processes that run on a Red Hat Enterprise Linux 7 operating system. You can orchestrate and scale your existing OpenShift workloads across on-prem and off-prem clouds for a portable, hybrid solution that works the same in multicloud scenarios. <br><br>
    To get started, try out the [Red Hat OpenShift on IBM Cloud tutorial](/docs/containers?topic=containers-openshift_tutorial).</dd>
</dl>

## Can I have a free OpenShift cluster?
{: #openshift_free}
{: faq}

You can create only standard OpenShift clusters. If you want to test out the capabilities of Kubernetes, [create a free Kubernetes cluster](/docs/containers?topic=containers-clusters#clusters_free) and [deploy some apps](/docs/containers?topic=containers-app). Then, re-deploy the apps you try out in the Kubernetes cluster to your [OpenShift cluster](/docs/containers?topic=containers-openshift_tutorial#openshift_deploy_app).

## Which Kubernetes versions does the OpenShift service support?
{: #supported_kube_versions}
{: faq}

The supported OpenShift version is 3.11, which includes Kubernetes 1.11.

## What am I charged for when I use an OpenShift? 
{: #charges}
{: faq}

For Red Hat OpenShift on IBM Cloud clusters, you are charged for the same components as in {{site.data.keyword.containerlong_notm}} clusters. For more information, see [What am I charged for when I use {{site.data.keyword.containerlong_notm}}?](/docs/containers?topic=containers-faqs#charges)

Additionally, your worker nodes are installed with the Red Hat Enterprise Linux operating system, which increases the price of the [worker node machines](/docs/containers?topic=containers-faqs#nodes). You must also have an OpenShift license, which incurs monthly costs in addition to the hourly VM costs or monthly bare metal costs. The OpenShift license is for every two cores of the worker node flavor. If you delete your worker node before the end of the month, your monthly license is available for other worker nodes in the worker pool to use.
