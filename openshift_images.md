---

copyright:
  years: 2014, 2019
lastupdated: "2019-07-16"

keywords: openshift, roks, rhoks, rhos

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
{:download: .download}
{:preview: .preview}

# Building images for your apps 
{: #openshift-images}

OpenShift are set up by default with a local Docker registry. If you want to use images that are stored in your remote private {{site.data.keyword.registrylong_notm}} `icr.io` domain names, you must create the secrets for each global and regional registry yourself. You can [copy the `default-<region>-icr-io` secrets](/docs/containers?topic=containers-images#copy_imagePullSecret) from the `default` namespace to the namespace that you want to pull images from, or [create your own secret](/docs/containers?topic=containers-images#other_registry_accounts). Then, [add the image pull secret](/docs/containers?topic=containers-images#use_imagePullSecret) to your deployment configuration or to the namespace service account.