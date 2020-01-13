---

copyright:
  years: 2014, 2020
lastupdated: "2020-01-08"

keywords: openshift, roks, rhos, rhoks, vlan

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


# Changing service endpoints
{: #cs_network_cluster}

After you initially set up your network when you [create a cluster](/docs/openshift?topic=openshift-clusters), you can change the service endpoints that your Kubernetes master is accessible through.
{: shortdesc}

In OpenShift clusters, you must enable the public service endpoint, and cannot later disable it. If no public service endpoint for the cluster exists, a subdomain for the router is not generated.
{: important}

## Setting up the private service endpoint
{: #set-up-private-se}

Enable or disable the private service endpoint for your cluster.
{: shortdesc}

The private service endpoint makes your Kubernetes master privately accessible. Your worker nodes and your authorized cluster users can communicate with the Kubernetes master over the private network. To determine whether you can enable the private service endpoint, see [Worker-to-master and user-to-master communication](/docs/openshift?topic=openshift-plan_clusters#workeruser-master). Note that you cannot disable the private service endpoint after you enable it.

Did you create a cluster with only a private service endpoint before you enabled your account for [VRF](/docs/resources?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud) and [service endpoints](/docs/account?topic=account-vrf-service-endpoint#service-endpoint)? Try [setting up the public service endpoint](#set-up-public-se) so that you can use your cluster until your support cases are processed to update your account.
{: tip}

1. Enable [VRF](/docs/resources?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud) in your IBM Cloud infrastructure account. To check whether a VRF is already enabled, use the `ibmcloud account show` command.
2. [Enable your {{site.data.keyword.cloud_notm}} account to use service endpoints](/docs/account?topic=account-vrf-service-endpoint#service-endpoint).
3. Enable the private service endpoint.
   ```
   ibmcloud oc cluster feature enable private-service-endpoint --cluster <cluster_name_or_ID>
   ```
   {: pre}
4. Refresh the Kubernetes master API server to use the private service endpoint. You can follow the prompt in the CLI, or manually run the following command. It might take several minutes for the master to refresh.
   ```
   ibmcloud oc cluster master refresh --cluster <cluster_name_or_ID>
   ```
   {: pre}

5. [Create a configmap](/docs/openshift?topic=openshift-update#worker-up-configmap) to control the maximum number of worker nodes that can be unavailable at a time in your cluster. When you update your worker nodes, the configmap helps prevent downtime for your apps as the apps are rescheduled orderly onto available worker nodes.
6. Update all the worker nodes in your cluster to pick up the private service endpoint configuration.

   <p class="important">By issuing the update command, the worker nodes are reloaded to pick up the service endpoint configuration. If no worker update is available, you must [reload the worker nodes manually](/docs/openshift?topic=openshift-kubernetes-service-cli). If you reload, be sure to cordon, drain, and manage the order to control the maximum number of worker nodes that are unavailable at a time.</p>
   ```
   ibmcloud oc worker update --cluster <cluster_name_or_ID> --worker <worker1,worker2>
   ```
   {: pre}

7. If the cluster is in an environment behind a firewall:
  * [Allow your authorized cluster users to run `kubectl` commands to access the master through the private service endpoint.](/docs/openshift?topic=openshift-firewall#firewall_kubectl)
  * [Allow outbound network traffic to the private IPs](/docs/openshift?topic=openshift-firewall#firewall_outbound) for infrastructure resources and for the {{site.data.keyword.cloud_notm}} services that you plan to use.



