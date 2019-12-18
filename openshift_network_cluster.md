---

copyright:
  years: 2014, 2019
lastupdated: "2019-12-18"

keywords: openshift, roks, rhos, rhoks, vlan

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

# Changing service endpoints
{: #cs_network_cluster}

After you initially set up your network when you [create a cluster](/docs/openshift?topic=openshift-clusters), you can change the service endpoints that your Kubernetes master is accessible through.
{: shortdesc}

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

9.  Optional: To use the private service endpoint only:
    1.  [Disable the public service endpoint](#disable-public-se).
    2.  [Set up access to the master on the private service endpoint](/docs/openshift?topic=openshift-access_cluster#access_private_se).


<br />


## Setting up the public service endpoint
{: #set-up-public-se}

Enable or disable the public service endpoint for your cluster.
{: shortdesc}

The public service endpoint makes your Kubernetes master publicly accessible. Your worker nodes and your authorized cluster users can securely communicate with the Kubernetes master over the public network. For more information, see [Worker-to-master and user-to-master communication](/docs/openshift?topic=openshift-plan_clusters#internet-facing).

**Steps to enable**</br>
If you previously disabled the public endpoint, you can re-enable it.
1. Enable the public service endpoint.
   ```
   ibmcloud oc cluster feature enable public-service-endpoint --cluster <cluster_name_or_ID>
   ```
   {: pre}
2. Refresh the Kubernetes master API server to use the public service endpoint. You can follow the prompt in the CLI, or manually run the following command. It might take several minutes for the master to refresh.
   ```
   ibmcloud oc cluster master refresh --cluster <cluster_name_or_ID>
   ```
   {: pre}
3. [Create a configmap](/docs/openshift?topic=openshift-update#worker-up-configmap) to control the maximum number of worker nodes that can be unavailable at a time in your cluster. When you update your worker nodes, the configmap helps prevent downtime for your apps as the apps are rescheduled orderly onto available worker nodes.
4. Update all the worker nodes in your cluster to remove the public service endpoint configuration.<p class="important">By issuing the update command, the worker nodes are reloaded to pick up the service endpoint configuration. If no worker update is available, you must reload the worker nodes manually with the `ibmcloud oc worker reload` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reload). If you reload, be sure to cordon, drain, and manage the order to control the maximum number of worker nodes that are unavailable at a time.</p>
   ```
   ibmcloud oc worker update --cluster <cluster_name_or_ID> --worker <worker1,worker2>
   ```
  {: pre}
   </br>

{: #disable-public-se}
**Steps to disable**</br>
To disable the public service endpoint, you must first enable the private service endpoint so that your worker nodes can communicate with the Kubernetes master.
1. [Enable the private service endpoint](#set-up-private-se).
2. Disable the public service endpoint.
   ```
   ibmcloud oc cluster feature disable public-service-endpoint --cluster <cluster_name_or_ID>
   ```
   {: pre}
3. Refresh the Kubernetes master API server to remove the public service endpoint by following the CLI prompt or by manually running the following command. It might take several minutes for the master to refresh.
   ```
   ibmcloud oc cluster master refresh --cluster <cluster_name_or_ID>
   ```
   {: pre}
4. [Create a configmap](/docs/openshift?topic=openshift-update#worker-up-configmap) to control the maximum number of worker nodes that can be unavailable at a time in your cluster. When you update your worker nodes, the configmap helps prevent downtime for your apps as the apps are rescheduled orderly onto available worker nodes.
5. Update all the worker nodes in your cluster to remove the public service endpoint configuration.<p class="important">By issuing the update command, the worker nodes are reloaded to pick up the service endpoint configuration. If no worker update is available, you must reload the worker nodes manually with the `ibmcloud oc worker reload` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reload). If you reload, be sure to cordon, drain, and manage the order to control the maximum number of worker nodes that are unavailable at a time.</p>
   ```
   ibmcloud oc worker update --cluster <cluster_name_or_ID> --worker <worker1,worker2>
   ```
  {: pre}

## Switching from the public service endpoint to the private service endpoint
{: #migrate-to-private-se}

Enable worker nodes to communicate with the master over the private network instead of the public network by enabling the private service endpoint.
{: shortdesc}

All clusters that are connected to a public and a private VLAN use the public service endpoint by default. Your worker nodes and your authorized cluster users can securely communicate with the Kubernetes master over the public network. To enable worker nodes to communicate with the Kubernetes master over the private network instead of the public network, you can enable the private service endpoint. Then, you can optionally disable the public service endpoint.
* If you enable the private service endpoint and keep the public service endpoint enabled too, workers always communicate with the master over the private network, but your users can communicate with the master over either the public or private network.
* If you enable the private service endpoint but disable the public service endpoint, workers and users must communicate with the master over the private network.

Note that you cannot disable the private service endpoint after you enable it.

1. Enable [VRF](/docs/resources?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud) in your IBM Cloud infrastructure account. To check whether a VRF is already enabled, use the `ibmcloud account show` command.
2. [Enable your {{site.data.keyword.cloud_notm}} account to use service endpoints](/docs/account?topic=account-vrf-service-endpoint#service-endpoint).
3. Enable the private service endpoint.
   ```
   ibmcloud oc cluster feature enable private-service-endpoint --cluster <cluster_name_or_ID>
   ```
   {: pre}
4. Refresh the Kubernetes master API server to use the private service endpoint by following the CLI prompt or by manually running the following command. It might take several minutes for the master to refresh.
   ```
   ibmcloud oc cluster master refresh --cluster <cluster_name_or_ID>
   ```
   {: pre}
5. [Create a configmap](/docs/openshift?topic=openshift-update#worker-up-configmap) to control the maximum number of worker nodes that can be unavailable at a time in your cluster. When you update your worker nodes, the configmap helps prevent downtime for your apps as the apps are rescheduled orderly onto available worker nodes.

6.  Update all the worker nodes in your cluster to pick up the private service endpoint configuration.

    <p class="important">By issuing the update command, the worker nodes are reloaded to pick up the service endpoint configuration. If no worker update is available, you must [reload the worker nodes manually](/docs/openshift?topic=openshift-kubernetes-service-cli). If you reload, be sure to cordon, drain, and manage the order to control the maximum number of worker nodes that are unavailable at a time.</p>
    ```
    ibmcloud oc worker update --cluster <cluster_name_or_ID> --worker <worker1,worker2>
    ```
    {: pre}

7.  Optional: To use the private service endpoint only:
    1.  Disable the public service endpoint.
        ```
        ibmcloud oc cluster feature disable public-service-endpoint --cluster <cluster_name_or_ID>
        ```
        {: pre}
    2.  [Set up access to the master on the private service endpoint](/docs/openshift?topic=openshift-access_cluster#access_private_se).



