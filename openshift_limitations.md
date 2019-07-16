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
{:important: .important}
{:deprecated: .deprecated}
{:download: .download}
{:preview: .preview}

# Service limitations
{: #openshift_limitations}

The Red Hat OpenShift on IBM Cloud beta is released with the following limitations. For general product limitations, such as API calls or number of pods per worker node, see [{{site.data.keyword.containerlong_notm}} service limitations](/docs/containers?topic=containers-ibm-cloud-kubernetes-service-technology#tech_limits).
{: shortdesc}

## Cluster
{: #oc_limits_cluster}

*   You can create only standard clusters, not free clusters. Instead, you can create a free Kubernetes cluster, and then re-deploy the apps you try out in the Kubernetes cluster to your OpenShift cluster.
*   Locations are available in two multizone metro areas, Washington, DC and London. Supported zones are `wdc04, wdc06, wdc07, lon04, lon05,` and `lon06`.
*   You cannot create a cluster with worker nodes that run multiple operating systems, such as OpenShift on Red Hat Enterprise Linux and native Kubernetes on Ubuntu.
*   The [cluster autoscaler](/docs/containers?topic=containers-ca) is not supported because it requires Kubernetes version 1.12 or later. OpenShift 3.11 includes only Kubernetes version 1.11.



## Storage
{: #oc_limits_storage}

{{site.data.keyword.cloud_notm}} file, block, and cloud object storage are supported. Portworx software-defined storage (SDS) is not supported.

Because of the way that {{site.data.keyword.cloud_notm}} NFS file storage configures Linux user permissions, you might encounter errors when you use file storage. If so, you might need to configure [OpenShift Security Context Constraints ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/admin_guide/manage_scc.html) or use a different storage type.

## Networking
{: #oc_limits_networking}

Calico is used as the networking policy provider instead of OpenShift SDN. To use Calico, you must download and edit the configuration file to use the master endpoint.
    1.  Download the Calico configuration file for your cluster. Note the file path in the output.
        ```
        ibmcloud ks cluster-config --cluster <cluster_name_or_ID> --network
        ```
        {: pre}

        Example output:
        ```
        The configuration for <cluster_name> was downloaded successfully.

        Network Config:

        /Users/<user_name>/.bluemix/plugins/container-service/clusters/<cluster_name>-admin/calicoctl.cfg
        ```
        {: screen}
    2.  Open the `calicoctl.cfg` file. In the `etcdEndpoints` field, remove the `-e` in the endpoint URL. For example, change `https://c1-e.<region>.containers.cloud.ibm.com:20357` to `https://c1.<region>.containers.cloud.ibm.com:20357`.
    3.  Save the `calicoctl.cfg` file.
    4.  Verify that Calico can connect to the cluster by listing the worker nodes. Depending on how Calico is set up on your operating system, you might need to include the file path to your `calicoctl.cfg` file in the `--config` flag.
        ```
        calicoctl get nodes --config <filepath_to_calicoctl.cfg>
        ```
        {: pre}
    5.  Repeat these steps each time that you need to download the Calico configuration file.

## Add-ons, integrations, and other services
{: #oc_limits_addons}

{{site.data.keyword.containerlong_notm}} add-ons such as Istio, Knative, and the Kubernetes terminal are not available.

Helm charts are not certified to work in OpenShift clusters, except {{site.data.keyword.cloud_notm}} Object Storage.

## Apps
{: #oc_limits_apps}

OpenShift sets up stricter security settings by default than native Kubernetes. 
*   For example, apps that are configured to run as root might fail, with the pods in a `CrashLoopBackOff` status. To resolve this issue, you can either modify the default security context constraints or use an image that does not run as root.
*  For more information, see the OpenShift docs for [Managing Security Context Constraints (SCC) ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.openshift.com/container-platform/3.11/admin_guide/manage_scc.html).

OpenShift are set up by default with a local Docker registry. If you want to use images that are stored in your remote private {{site.data.keyword.registrylong_notm}} `icr.io` domain names, you must create the secrets for each global and regional registry yourself. You can [copy the `default-<region>-icr-io` secrets](/docs/containers?topic=containers-images#copy_imagePullSecret) from the `default` namespace to the namespace that you want to pull images from, or [create your own secret](/docs/containers?topic=containers-images#other_registry_accounts). Then, [add the image pull secret](/docs/containers?topic=containers-images#use_imagePullSecret) to your deployment configuration or to the namespace service account.

The OpenShift console is used instead of the Kubernetes dashboard.
