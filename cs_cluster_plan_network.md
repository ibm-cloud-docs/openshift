---

copyright:
  years: 2014, 2019
lastupdated: "2019-07-26"

keywords: kubernetes, iks, multi az, multi-az, szr, mzr

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


# Planning your cluster network setup
{: #plan_clusters}

Design a network setup for your Kubernetes clusters in {{site.data.keyword.containerlong}} that meets the needs of your workloads and environment.
{: shortdesc}

Your containerized apps are hosted on compute hosts that are called worker nodes. Worker nodes are managed by the Kubernetes master. The communication setup between worker nodes and the Kubernetes master, other services, the Internet, or other private networks depends on how you set up your IBM Cloud infrastructure network.

First time creating a cluster? First, try out the [creating Kubernetes clusters tutorial](/docs/containers?topic=containers-cs_cluster_tutorial). Then, come back here when you’re ready to plan out your production-ready clusters.
{: tip}

