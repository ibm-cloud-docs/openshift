---

copyright:
  years: 2014, 2020
lastupdated: "2020-02-24"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift

---

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


# FAQs
{: #faqs}

Review frequently asked questions for using {{site.data.keyword.openshiftlong}}.
{: shortdesc}

## What container platforms are available for my cluster?
{: #container_platforms}
{: faq}
{: support}

With {{site.data.keyword.cloud_notm}}, you have a choice between two different container management platforms: the IBM version of community Kubernetes and Red Hat OpenShift on IBM Cloud. The container platform that you select is installed on your cluster master and worker nodes. Later, you can [update the version](/docs/openshift?topic=openshift-update) but cannot roll back to a previous version or switch to a different container platform. If you want to use multiple container platforms, create a separate cluster for each.

For more information, see [Comparison between OpenShift and community Kubernetes clusters](/docs/openshift?topic=openshift-cs_ov#openshift_kubernetes).

<dl>
  <dt>Kubernetes</dt>
    <dd>[Kubernetes ![External link icon](../icons/launch-glyph.svg "External link icon")](https://kubernetes.io/) is a open source project that you can use to automate, scale, and manage your containerized apps. With the [{{site.data.keyword.containerlong_notm}} version](/docs/openshift?topic=openshift-openshift_versions), you get access to community Kubernetes API features that are considered **beta** or higher by the community. Kubernetes **alpha** features, which are subject to change, are generally not enabled by default. You can run your apps on an Ubuntu worker node in {{site.data.keyword.cloud_notm}}. With Kubernetes, you can combine various resources such as secrets, deployments, and services to securely create and manage highly available, containerized apps.<br><br>
    To get started, [create a Kubernetes cluster](/docs/containers?topic=containers-cs_cluster_tutorial).</dd>
  <dt>OpenShift</dt>
    <dd>Red Hat OpenShift on IBM Cloud is a Kubernetes-based platform that is designed especially to accelerate your containerized app delivery processes that run on a Red Hat Enterprise Linux 7 operating system. You can orchestrate and scale your existing OpenShift workloads across on-prem and off-prem clouds for a portable, hybrid solution that works the same in multicloud scenarios. <br><br>
    To get started, try out the [Red Hat OpenShift on IBM Cloud tutorial](/docs/openshift?topic=openshift-openshift_tutorial).</dd>
</dl>

## Can I create a free OpenShift cluster?
{: #openshift_free}
{: faq}
{: support}


You can create only standard OpenShift clusters. If you want to test out the capabilities of Kubernetes, [create a free Kubernetes cluster](/docs/containers?topic=containers-getting-started) and [deploy some apps](/docs/containers?topic=containers-app). Then, redeploy the apps that you try out in the Kubernetes cluster to your [OpenShift cluster](/docs/openshift?topic=openshift-openshift_tutorial#openshift_deploy_app).

## Which Kubernetes versions does the OpenShift service support?
{: #supported_kube_versions}
{: faq}
{: support}

Red Hat OpenShift on IBM Cloud supports the following versions of OpenShift. The worker node operating system is Red Hat Enterprise Linux 7.

* **Default**: 3.11, which includes Kubernetes 1.11
* **Latest**: 4.3, which includes Kubernetes 1.16

## What am I charged for when I use an OpenShift cluster?
{: #openshift_charges}
{: faq}
{: support}

For Red Hat OpenShift on IBM Cloud clusters, you are charged for the same components as in {{site.data.keyword.containerlong_notm}} clusters. For more information, see [What am I charged for when I use {{site.data.keyword.containerlong_notm}}?](/docs/containers?topic=containers-faqs#charges) Additionally, your OpenShift clusters include charges for extra compute and storage resources.

<img src="images/icon-version-43.png" alt="Version 4.3 icon" width="30" style="width:30px; border-style: none"/> <img src="images/icon-beta-flair.png" alt="Beta icon" width="30" style="width:30px; border-style: none"/> Red Hat OpenShift on IBM Cloud version 4.3 is available as a beta. During the beta, the OpenShift license fee is waived. Any 4.3 beta clusters that you create remain for only 30 days after the beta ends and version 4.3 becomes generally available. Beta releases have limited features and might experience intermittent errors. For more information, review the [troubleshooting](/docs/openshift?topic=openshift-cs_troubleshoot), [limitations](/docs/openshift?topic=openshift-openshift_limitations#ocp4_limitations), and [internal](https://ibm-argonauts.slack.com/archives/CJH0UPN2D){: external} or [external](https://ibm-container-service.slack.com/archives/CKCJLJCH4){: external} Slack channel.
{: preview}

**Compute**<br>
Your worker nodes are installed with the Red Hat Enterprise Linux operating system, which includes a license for each worker node. To use Red Hat OpenShift Container Platform, an OpenShift license is also included, which incurs monthly costs in addition to the costs of your worker nodes.

An OpenShift license is billed for every four virtual cores (or two physical cores) of the worker node flavor. You are charged for the entire license for each month that you have worker nodes in a `deployed` state. For example, if you create the cluster on 15 August and delete the cluster on 14 September, you are still charged for the OCP licenses for two monthly periods: August and September.

* If you delete your worker node before the end of the month, your monthly license is available for other worker nodes in the same worker pool to use.
* If you delete the cluster before the end of the month, you are still charged the entire monthly price for the OpenShift license.

**Storage**<br>
To store images in the internal registry, a classic {{site.data.keyword.cloud_notm}} File Storage volume is automatically created for you. Your file storage volume is provisioned with 20 GB capacity at 2 IOPS/GB, and billed hourly. If you need more image storage capacity, you can [update the volume size](/docs/openshift?topic=openshift-registry#storage_internal_registry), which modifies the cost. For more information, see [Billing](/docs/FileStorage?topic=FileStorage-about).

## Can I add tags to my cluster?
{: #faq_tags}
{: faq}

Yes, you can add tags to your cluster to help organize your {{site.data.keyword.cloud_notm}} resources such as for billing purposes. For more information, see [Adding tags to existing clusters](/docs/openshift?topic=openshift-add_workers#cluster_tags).
