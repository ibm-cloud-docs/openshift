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
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:preview: .preview}

# Service limitations
{: #openshift_limitations}

The {{site.data.keyword.openshiftlong}} beta is released with the following limitations. For general product limitations, such as API calls or number of pods per worker node, see [{{site.data.keyword.containerlong_notm}} service limitations](/docs/containers?topic=containers-ibm-cloud-kubernetes-service-technology#tech_limits).
{: shortdesc}

## Cluster
{: #oc_limits_cluster}

*   You can create only standard clusters, not free clusters. Instead, you can create a free Kubernetes cluster, and then re-deploy the apps you try out in the Kubernetes cluster to your OpenShift cluster.
*   Locations are available in two multizone metro areas, Washington, DC and London. Supported zones are `wdc04, wdc06, wdc07, lon04, lon05,` and `lon06`.
*   You cannot create a cluster with worker nodes that run multiple operating systems, such as OpenShift on Red Hat Enterprise Linux and community Kubernetes on Ubuntu.



## Storage
{: #oc_limits_storage}

{{site.data.keyword.cloud_notm}} file, block, and cloud object storage are supported. Portworx software-defined storage (SDS) is not supported.

Because of the way that {{site.data.keyword.cloud_notm}} NFS file storage configures Linux user permissions, you might encounter errors when you use file storage. If so, you might need to configure [OpenShift Security Context Constraints ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/admin_guide/manage_scc.html) or use a different storage type.
