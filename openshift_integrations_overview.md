---

copyright:
  years: 2014, 2025
lastupdated: "2025-10-17"


keywords: kubernetes, openshift

subcollection: openshift

---


{{site.data.keyword.attribute-definition-list}}




# Supported IBM Cloud and third-party integrations
{: #supported_integrations}

Learn more about the following {{site.data.keyword.IBM}}, {{site.data.keyword.cloud}}, and third-party integrations for {{site.data.keyword.openshiftlong_notm}} clusters.
{: shortdesc}

|Service|Description|
|----|----|
| {{site.data.keyword.cloud_notm}} platform services | {{site.data.keyword.cloud_notm}} platform services that support service keys can be integrated by using [service binding](/docs/openshift?topic=openshift-service-binding). |
| {{site.data.keyword.cloud_notm}} classic infrastructure services | Your {{site.data.keyword.redhat_openshift_notm}} cluster is based on fully integrated {{site.data.keyword.cloud_notm}} classic infrastructure services such as Virtual Servers, Bare Metal Servers, or VLANs. You create and work with these services instances by using the {{site.data.keyword.containerlong_notm}} API, CLI, or console. To secure your cluster network or connect to an on-prem data center, you can configure one of the following options:  \n - [strongSwan IPSec VPN Service](/docs/openshift?topic=openshift-vpn#vpn-setup)  \n - [{{site.data.keyword.BluDirectLink}}](/docs/dl?topic=dl-get-started-with-ibm-cloud-dl)  \n - [Virtual Router Appliance (VRA)](/docs/openshift?topic=openshift-vpn#vyatta) |
| {{site.data.keyword.cloud_notm}} storage | Supported persistent storage solutions, such as {{site.data.keyword.cloud_notm}} {{site.data.keyword.filestorage_short}}, {{site.data.keyword.cloud_notm}} Block Storage, or {{site.data.keyword.cos_full_notm}} are integrated as Kubernetes drivers and can be set up by using Helm charts. The storage documentation for each solution includes instructions to install and manage storage. For more information about choosing a persistent storage solution, see [Planning highly available persistent storage](/docs/openshift?topic=openshift-storage-plan). |
| Cluster autoscaler | With the `ibm-iks-cluster-autoscaler` plug-in, you can scale the worker pools in your cluster automatically to increase or decrease the number of worker nodes in the worker pool based on the sizing requests of your scheduled workloads. For more information, see [Scaling clusters](/docs/openshift?topic=openshift-cluster-scaling-install-addon). |
| Diagnostics and debug tool | While you troubleshoot, you can use the [{{site.data.keyword.containerlong_notm}} Diagnostics and Debug Tool add-on](/docs/openshift?topic=openshift-debug-tool) to run tests and gather pertinent information from your cluster. |
| IBM Cloud Paks | [IBM Cloud Paks&trade;](https://www.ibm.com/products/cloud-paks){: external} are containerized, licensed IBM middleware and open source software components that you can use to modernize, move, and build cloud-native business applications in hybrid and multicloud deployments. By running exclusively on {{site.data.keyword.redhat_openshift_notm}} and Red Hat Enterprise Linux, Cloud Paks are built atop a secure stack and maintain consistency in deployment and behavior across cloud providers. To get started, see [Adding Cloud Paks](/docs/openshift?topic=openshift-openshift_cloud_paks). |
| Istio for service mesh | Unlike for community Kubernetes clusters, the Istio managed add-on is not supported. Instead, use the Red Hat service mesh operator. **Note**: The default {{site.data.keyword.cloud_notm}} configuration of the routers enables host networking, which is not compatible with the service mesh network policy. For the service mesh ingress to work, [apply a network policy](https://gist.githubusercontent.com/kitch/39c504a2ed9e381c2aadea436d5b52e4/raw/d8efa69f41d41425b16bb363a881a98d40d3708c/mesh-policy.yaml){: external}. For more information, see [Service Mesh 3.x](https://docs.redhat.com/en/documentation/openshift_container_platform/4.18/html/service_mesh/service-mesh-3-x){: external} and [Red Hat OpenShift Service Mesh 3.0](https://docs.redhat.com/en/documentation/red_hat_openshift_service_mesh/3.0){: external}. |
| {{site.data.keyword.logs_full_notm}} | Add log management capabilities to your cluster by deploying an {{site.data.keyword.logs_full_notm}} agent to your worker nodes to manage logs from your pod containers. For more information, see the following docs.  \n - [Setting up {{site.data.keyword.logs_full_notm}} in a {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/cloud-logs?topic=cloud-logs-agent-helm-os-deploy).|
| Portworx | [Portworx](https://portworx.com/products/portworx-enterprise){: external} is a highly available software-defined storage solution that you can use to manage persistent storage for your containerized databases and other stateful apps, or to share data between pods across multiple zones. You can [install Portworx with a Helm chart](/docs/openshift?topic=openshift-storage_portworx_about) and provision storage for your apps by using Kubernetes persistent volumes. However, the default configuration requires that you modify the security context constraints. |
| {{site.data.keyword.mon_full_notm}} | Gain operational visibility into the performance and health of your apps by deploying a {{site.data.keyword.mon_short}} agent to your worker nodes to forward metrics to {{site.data.keyword.mon_full}}. For more information, see the following docs.  \n - [Setting up {{site.data.keyword.mon_full_notm}} in a {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-health-monitor).  \n - [Tutorial: Analyzing metrics for an app that is deployed in a Kubernetes cluster](/docs/monitoring?topic=monitoring-kubernetes_cluster#kubernetes_cluster). |
| Other third-party integrations | You can install many other integrations into your {{site.data.keyword.redhat_openshift_notm}} cluster, such as through the {{site.data.keyword.redhat_openshift_notm}} catalog, Operators, Helm charts, or do-it-yourself open source software installations. Make sure that these apps are compatible with your {{site.data.keyword.redhat_openshift_notm}} cluster and Kubernetes version. For example, you might need to [update the app](/docs/openshift?topic=openshift-plan_deploy#openshift_move_apps_scenarios) for the installation to succeed. |
{: caption="{{site.data.keyword.cloud_notm}} and third-party integrations for {{site.data.keyword.openshiftlong}} clusters"}
{: summary=""}
