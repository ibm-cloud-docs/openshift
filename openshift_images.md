---

copyright:
  years: 2014, 2019
lastupdated: "2019-07-19"

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

# Building images for your apps 
{: #openshift-images}

Red Hat OpenShift on IBM Cloud clusters include an internal registry to build, deploy, and manage container images locally. For a private registry to manage and control access to images across your enterprise, you can also set up your cluster to use {{site.data.keyword.registrylong}}.
{: shortdesc}

## Using the internal registry
{: #openshift_internal_registry}

OpenShift clusters are set up by default with an internal registry. For more information, see the [OpenShift docs ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/install_config/registry/index.html#install-config-registry-overview).
{: shortdesc}

## Using {{site.data.keyword.registrylong_notm}}
{: #openshift_iccr}

If you want to use images that are stored in your remote private {{site.data.keyword.registrylong_notm}} `icr.io` domain names, you must create image pull secrets for each global and regional registry. Then, add the image pull secrets to each project, and to a service account for each project or to each deployment.
{: shortdesc}

For information, see the following topics in the {{site.data.keyword.containershort_notm}} docs.
* [Understanding how to authorize your cluster to pull images from a registry](/docs/containers?topic=containers-images#cluster_registry_auth).
* [Copying the `default-<region>-icr-io` secrets](/docs/containers?topic=containers-images#copy_imagePullSecret) from the `default` namespace to the namespace that you want to pull images from.
* [Creating your own image pull secret](/docs/containers?topic=containers-images#other_registry_accounts).
* [Adding the image pull secret](/docs/containers?topic=containers-images#use_imagePullSecret) to your deployment configuration or to the namespace service account.