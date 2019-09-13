---

copyright:
  years: 2014, 2019
lastupdated: "2019-09-13"

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

With {{site.data.keyword.containerlong_notm}}, you can select from two container management platforms: the IBM version of community Kubernetes and Red Hat OpenShift on IBM Cloud. The container platform that you select is installed on your cluster master and worker nodes. Later, you can [update the version](/docs/containers?topic=containers-update#update) but cannot roll back to a previous version or switch to a different container platform. If you want to use multiple container platforms, create a separate cluster for each.

For more information, see [Comparison between OpenShift and community Kubernetes clusters](/docs/openshift?topic=openshift-why_openshift#openshift_kubernetes).

<dl>
  <dt>Kubernetes</dt>
    <dd>[Kubernetes ![External link icon](../icons/launch-glyph.svg "External link icon")](https://kubernetes.io/) is a production-grade, open source container orchestration platform that you can use to automate, scale, and manage your containerized apps that run on an Ubuntu operating system. With the [{{site.data.keyword.containerlong_notm}} version](/docs/containers?topic=containers-cs_versions#cs_versions), you get access to community Kubernetes API features that are considered **beta** or higher by the community. Kubernetes **alpha** features, which are subject to change, are generally not enabled by default. With Kubernetes, you can combine various resources such as secrets, deployments, and services to securely create and manage highly available, containerized apps.<br><br>
    To get started, [create a Kubernetes cluster](/docs/containers?topic=containers-cs_cluster_tutorial#cs_cluster_tutorial).</dd>
  <dt>OpenShift</dt>
    <dd>Red Hat OpenShift on IBM Cloud is a Kubernetes-based platform that is designed especially to accelerate your containerized app delivery processes that run on a Red Hat Enterprise Linux 7 operating system. You can orchestrate and scale your existing OpenShift workloads across on-prem and off-prem clouds for a portable, hybrid solution that works the same in multicloud scenarios. <br><br>
    To get started, try out the [Red Hat OpenShift on IBM Cloud tutorial](/docs/openshift?topic=openshift-openshift_tutorial).</dd>
</dl>

## Can I create a free OpenShift cluster?
{: #openshift_free}
{: faq}

You can create only standard OpenShift clusters. If you want to test out the capabilities of Kubernetes, [create a free Kubernetes cluster](/docs/containers?topic=containers-getting-started#clusters_gs) and [deploy some apps](/docs/containers?topic=containers-app). Then, re-deploy the apps that you try out in the Kubernetes cluster to your [OpenShift cluster](/docs/openshift?topic=openshift-openshift_tutorial#openshift_deploy_app).

## Which Kubernetes versions does the OpenShift service support?
{: #supported_kube_versions}
{: faq}

The supported OpenShift version is 3.11, which includes Kubernetes 1.11.

## What am I charged for when I use an OpenShift cluster?
{: #openshift_charges}
{: faq}

For Red Hat OpenShift on IBM Cloud clusters, you are charged for the same components as in {{site.data.keyword.containerlong_notm}} clusters. For more information, see [What am I charged for when I use {{site.data.keyword.containerlong_notm}}?](/docs/containers?topic=containers-faqs#charges) Additionally, your OpenShift clusters include charges for extra compute and storage resources.

**Compute**: Your worker nodes are installed with the Red Hat Enterprise Linux operating system, which includes a license for each worker node. The cost of this license is added to the cost of your worker nodes. To use Red Hat OpenShift Container Platform, an OpenShift license is also included, which incurs monthly costs in addition to the costs of your worker nodes. 

The OpenShift license is for every two cores of the worker node flavor. The monthly license is not prorated, but charged in 30-day increments. You are charged for the entire monthly license even if you delete resources before the 30-day period.  For example, if you create the cluster on 15 August and delete the cluster on 27 August, you are still charged for the OCP licenses for the 15 August - 15 September time period.

* If you delete your worker node before the end of the 30-day period, your monthly license is available for other worker nodes in the same worker pool to use. 
* If you delete the cluster before the end of the 30-day period, you are still charged the entire monthly price for the OpenShift license.

**Storage**: To store images in the internal registry, a classic {{site.data.keyword.cloud_notm}} File Storage volume is automatically created for you. Your file storage volume is provisioned with 20 GB capacity at 2 IOPS/GB, and billed hourly. If you need more image storage capacity, you can [update the volume size](/docs/openshift?topic=openshift-openshift-images#storage_internal_registry), which modifies the cost. For more information on the cost, see [Billing](/docs/infrastructure/FileStorage?topic=FileStorage-about).
