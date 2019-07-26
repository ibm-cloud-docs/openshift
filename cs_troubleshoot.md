---

copyright:
  years: 2014, 2019
lastupdated: "2019-07-26"

keywords: kubernetes, iks
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
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}



# Debugging your cluster
{: #cs_troubleshoot}

As you use {{site.data.keyword.containerlong}}, consider these techniques for general troubleshooting and debugging your community Kubernetes or OpenShift clusters. You can also check the [status of the {{site.data.keyword.cloud_notm}} system ![External link icon](../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/bluemix/support/#status).
{: shortdesc}

You can take these general steps to ensure that your clusters are up-to-date:
- Check monthly for available security and operating system patches to [update your worker nodes](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_worker_update).
- [Update your cluster](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_cluster_update) to the latest default version for [community Kubernetes](/docs/containers?topic=containers-cs_versions) or [OpenShift](/docs/containers?topic=containers-cs_versions).<p class="important">Make sure that [your `kubectl` CLI](/docs/containers?topic=containers-cs_cli_install#kubectl) client matches the same Kubernetes version as your cluster server. [Kubernetes does not support ![External link icon](../icons/launch-glyph.svg "External link icon")](https://kubernetes.io/docs/setup/version-skew-policy/) `kubectl` client versions that are 2 or more versions apart from the server version (n +/- 2).</p>

## Running tests with the {{site.data.keyword.containerlong_notm}} Diagnostics and Debug Tool
{: #debug_utility}

While you troubleshoot, you can use the {{site.data.keyword.containerlong_notm}} Diagnostics and Debug Tool to run tests and gather pertinent information from your cluster. To use the debug tool, install the [`ibmcloud-iks-debug` Helm chart ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/kubernetes/helm/iks-charts/ibmcloud-iks-debug):
{: shortdesc}


1. [Set up Helm in your cluster, create a service account for Tiller, and add the `ibm` repository to your Helm instance](/docs/containers?topic=containers-helm).

2. Install the Helm chart to your cluster.
  ```
  helm install iks-charts/ibmcloud-iks-debug --name debug-tool
  ```
  {: pre}

3. Start a proxy server to display the debug tool interface.
  ```
  kubectl proxy --port 8080
  ```
  {: pre}

4. In a web browser, open the debug tool interface URL: http://localhost:8080/api/v1/namespaces/default/services/debug-tool-ibmcloud-iks-debug:8822/proxy/page

5. Select individual tests or a group of tests to run. Some tests check for potential warnings, errors, or issues, and some tests only gather information that you can reference while you troubleshoot. For more information about the function of each test, click the information icon next to the test's name.

6. Click **Run**.

7. Check the results of each test.
  * If any test fails, click the information icon next to the test's name in the left column for information about how to resolve the issue.
  * You can also use the results of tests to gather information, such as complete YAMLs, that can help you debug your cluster in the following sections.

## Debugging clusters
{: #debug_clusters}

Review the options to debug your clusters and find the root causes for failures.

1.  List your cluster and find the `State` of the cluster.

  ```
  ibmcloud ks clusters
  ```
  {: pre}

2.  Review the `State` of your cluster. If your cluster is in a **Critical**, **Delete failed**, or **Warning** state, or is stuck in the **Pending** state for a long time, start [debugging the worker nodes](#debug_worker_nodes).

    You can view the current cluster state by running the `ibmcloud ks clusters` command and locating the **State** field. 
{: shortdesc}

<table summary="Every table row should be read left to right, with the cluster state in column one and a description in column two.">
<caption>Cluster states</caption>
   <thead>
   <th>Cluster state</th>
   <th>Description</th>
   </thead>
   <tbody>
<tr>
   <td>`Aborted`</td>
   <td>The deletion of the cluster is requested by the user before the Kubernetes master is deployed. After the deletion of the cluster is completed, the cluster is removed from your dashboard. If your cluster is stuck in this state for a long time, open an [{{site.data.keyword.cloud_notm}} support case](/docs/containers?topic=containers-cs_troubleshoot#ts_getting_help).</td>
   </tr>
 <tr>
     <td>`Critical`</td>
     <td>The Kubernetes master cannot be reached or all worker nodes in the cluster are down. If you enabled {{site.data.keyword.keymanagementservicelong_notm}} in your cluster, the {{site.data.keyword.keymanagementserviceshort}} container might fail to encrypt or decrypt your cluster secrets. If so, you can view an error with more information when you run `{[kubectl]} get secrets`.</td>
    </tr>
   <tr>
     <td>`Delete failed`</td>
     <td>The Kubernetes master or at least one worker node cannot be deleted.  </td>
   </tr>
   <tr>
     <td>`Deleted`</td>
     <td>The cluster is deleted but not yet removed from your dashboard. If your cluster is stuck in this state for a long time, open an [{{site.data.keyword.cloud_notm}} support case](/docs/containers?topic=containers-cs_troubleshoot#ts_getting_help). </td>
   </tr>
   <tr>
   <td>`Deleting`</td>
   <td>The cluster is being deleted and cluster infrastructure is being dismantled. You cannot access the cluster.  </td>
   </tr>
   <tr>
     <td>`Deploy failed`</td>
     <td>The deployment of the Kubernetes master could not be completed. You cannot resolve this state. Contact IBM Cloud support by opening an [{{site.data.keyword.cloud_notm}} support case](/docs/containers?topic=containers-cs_troubleshoot#ts_getting_help).</td>
   </tr>
     <tr>
       <td>`Deploying`</td>
       <td>The Kubernetes master is not fully deployed yet. You cannot access your cluster. Wait until your cluster is fully deployed to review the health of your cluster.</td>
      </tr>
      <tr>
       <td>`Normal`</td>
       <td>All worker nodes in a cluster are up and running. You can access the cluster and deploy apps to the cluster. This state is considered healthy and does not require an action from you.<p class="note">Although the worker nodes might be normal, other infrastructure resources, such as [networking](/docs/containers?topic=containers-cs_troubleshoot_network) and [storage](/docs/containers?topic=containers-cs_troubleshoot_storage), might still need attention. If you just created the cluster, some parts of the cluster that are used by other services such as Ingress secrets or registry image pull secrets, might still be in process.</p></td>
    </tr>
      <tr>
       <td>`Pending`</td>
       <td>The Kubernetes master is deployed. The worker nodes are being provisioned and are not available in the cluster yet. You can access the cluster, but you cannot deploy apps to the cluster.  </td>
     </tr>
   <tr>
     <td>`Requested`</td>
     <td>A request to create the cluster and order the infrastructure for the Kubernetes master and worker nodes is sent. When the deployment of the cluster starts, the cluster state changes to <code>Deploying</code>. If your cluster is stuck in the <code>Requested</code> state for a long time, open an [{{site.data.keyword.cloud_notm}} support case](/docs/containers?topic=containers-cs_troubleshoot#ts_getting_help). </td>
   </tr>
   <tr>
     <td>`Updating`</td>
     <td>The Kubernetes API server that runs in your Kubernetes master is being updated to a new Kubernetes API version. During the update, you cannot access or change the cluster. Worker nodes, apps, and resources that the user deployed are not modified and continue to run. Wait for the update to complete to review the health of your cluster. </td>
   </tr>
   <tr>
    <td>`Unsupported`</td>
    <td>The [Kubernetes version](/docs/containers?topic=containers-cs_versions#cs_versions) that the cluster runs is no longer supported. Your cluster's health is no longer actively monitored or reported. Additionally, you cannot add or reload worker nodes. To continue receiving important security updates and support, you must update your cluster. Review the [version update preparation actions](/docs/containers?topic=containers-cs_versions#prep-up), then [update your cluster](/docs/containers?topic=containers-update#update) to a supported Kubernetes version.<br><br><p class="note">Clusters that are three or more versions behind the oldest supported version cannot be updated. To avoid this situation, you can update the cluster to a Kubernetes version less than three ahead of the current version, such as 1.12 to 1.14. Further, if your cluster runs version 1.5, 1.7, or 1.8, then the version is too far behind to update. Instead, you must [create a cluster](/docs/containers?topic=containers-clusters#clusters) and [deploy your apps](/docs/containers?topic=containers-app#app) to the cluster.</p></td>
   </tr>
    <tr>
       <td>`Warning`</td>
       <td><ul><li>At least one worker node in the cluster is not available, but other worker nodes are available and can take over the workload. Try to [reload](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_worker_reload) the unavailable worker nodes.</li>
       <li>Your cluster has zero worker nodes, such as if you created a cluster without any worker nodes or manually removed all the worker nodes from the cluster. [Resize your worker pool](/docs/containers?topic=containers-add_workers#resize_pool) to add worker nodes to recover from a `Warning` state.</li>
       <li>A control plane operation for your cluster failed. View the cluster in the console or run `ibmcloud ks cluster-get --cluster <cluster_name_or_ID>` to [check the **Master Status** for further debugging](/docs/containers?topic=containers-cs_troubleshoot#debug_master).</li></ul></td>
    </tr>
   </tbody>
 </table>


The [Kubernetes master](/docs/containers?topic=containers-ibm-cloud-kubernetes-service-technology#architecture) is the main component that keeps your cluster up and running. The master stores cluster resources and their configurations in the etcd database that serves as the single point of truth for your cluster. The Kubernetes API server is the main entry point for all cluster management requests from the worker nodes to the master, or when you want to interact with your cluster resources.<br><br>If a master failure occurs, your workloads continue to run on the worker nodes, but you cannot use `{[kubectl]}` commands to work with your cluster resources or view the cluster health until the Kubernetes API server in the master is back up. If a pod goes down during the master outage, the pod cannot be rescheduled until the worker node can reach the Kubernetes API server again.<br><br>During a master outage, you can still run `ibmcloud ks` commands against the {{site.data.keyword.containerlong_notm}} API to work with your infrastructure resources, such as worker nodes or VLANs. If you change the current cluster configuration by adding or removing worker nodes to the cluster, your changes do not happen until the master is back up.

Do not restart or reboot a worker node during a master outage. This action removes the pods from your worker node. Because the Kubernetes API server is unavailable, the pods cannot be rescheduled onto other worker nodes in the cluster.
{: important}


<br />


## Debugging worker nodes
{: #debug_worker_nodes}

Review the options to debug your worker nodes and find the root causes for failures.

<ol><li>If your cluster is in a **Critical**, **Delete failed**, or **Warning** state, or is stuck in the **Pending** state for a long time, review the state of your worker nodes.<p class="pre">ibmcloud ks workers --cluster <cluster_name_or_id></p></li>
<li>Review the **State** and **Status** field for every worker node in your CLI output.<p>You can view the current worker node state by running the `ibmcloud ks workers --cluster <cluster_name_or_ID` command and locating the **State** and **Status** fields.
{: shortdesc}

<table summary="Every table row should be read left to right, with the cluster state in column one and a description in column two.">
<caption>Worker node states</caption>
  <thead>
  <th>Worker node state</th>
  <th>Description</th>
  </thead>
  <tbody>
<tr>
    <td>`Critical`</td>
    <td>A worker node can go into a Critical state for many reasons: <ul><li>You initiated a reboot for your worker node without cordoning and draining your worker node. Rebooting a worker node can cause data corruption in <code>containerd</code>, <code>kubelet</code>, <code>kube-proxy</code>, and <code>calico</code>. </li>
    <li>The pods that are deployed to your worker node do not use resource limits for [memory ![External link icon](../icons/launch-glyph.svg "External link icon")](https://kubernetes.io/docs/tasks/configure-pod-container/assign-memory-resource/) and [CPU ![External link icon](../icons/launch-glyph.svg "External link icon")](https://kubernetes.io/docs/tasks/configure-pod-container/assign-cpu-resource/). Without resource limits, pods can consume all available resources, leaving no resources for other pods to run on this worker node. This overcommitment of workload causes the worker node to fail. </li>
    <li><code>containerd</code>, <code>kubelet</code>, or <code>calico</code> went into an unrecoverable state after it ran hundreds or thousands of containers over time. </li>
    <li>You set up a Virtual Router Appliance for your worker node that went down and cut off the communication between your worker node and the Kubernetes master. </li><li> Current networking issues in {{site.data.keyword.containerlong_notm}} or IBM Cloud infrastructure that causes the communication between your worker node and the Kubernetes master to fail.</li>
    <li>Your worker node ran out of capacity. Check the <strong>Status</strong> of the worker node to see whether it shows <strong>Out of disk</strong> or <strong>Out of memory</strong>. If your worker node is out of capacity, consider to either reduce the workload on your worker node or add a worker node to your cluster to help load balance the workload.</li>
    <li>The device was powered off from the [{{site.data.keyword.cloud_notm}} console resource list ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/resources). Open the resource list and find your worker node ID in the **Devices** list. In the action menu, click **Power On**.</li></ul>
    In many cases, [reloading](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_worker_reload) your worker node can solve the problem. When you reload your worker node, the latest [patch version](/docs/containers?topic=containers-cs_versions#version_types) is applied to your worker node. The major and minor version is not changed. Before you reload your worker node, make sure to cordon and drain your worker node to ensure that the existing pods are terminated gracefully and rescheduled onto remaining worker nodes. </br></br> If reloading the worker node does not resolve the issue, go to the next step to continue troubleshooting your worker node. </br></br><strong>Tip:</strong> You can [configure health checks for your worker node and enable Autorecovery](/docs/containers?topic=containers-health#autorecovery). If Autorecovery detects an unhealthy worker node based on the configured checks, Autorecovery triggers a corrective action like an OS reload on the worker node. For more information about how Autorecovery works, see the [Autorecovery blog ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/blogs/bluemix/2017/12/autorecovery-utilizes-consistent-hashing-high-availability/).
    </td>
   </tr>
   <tr>
   <td>`Deployed`</td>
   <td>Updates are successfully deployed to your worker node. After updates are deployed, {{site.data.keyword.containerlong_notm}} starts a health check on the worker node. After the health check is successful, the worker node goes into a <code>Normal</code> state. Worker nodes in a <code>Deployed</code> state usually are ready to receive workloads, which you can check by running <code>{[kubectl]} get nodes</code> and confirming that the state shows <code>Normal</code>. </td>
   </tr>
    <tr>
      <td>`Deploying`</td>
      <td>When you update the Kubernetes version of your worker node, your worker node is redeployed to install the updates. If you reload or reboot your worker node, the worker node is redeployed to automatically install the latest patch version. If your worker node is stuck in this state for a long time, continue with the next step to see whether a problem occurred during the deployment. </td>
   </tr>
      <tr>
      <td>`Normal`</td>
      <td>Your worker node is fully provisioned and ready to be used in the cluster. This state is considered healthy and does not require an action from the user. **Note**: Although the worker nodes might be normal, other infrastructure resources, such as [networking](/docs/containers?topic=containers-cs_troubleshoot_network) and [storage](/docs/containers?topic=containers-cs_troubleshoot_storage), might still need attention.</td>
   </tr>
 <tr>
      <td>`Provisioning`</td>
      <td>Your worker node is being provisioned and is not available in the cluster yet. You can monitor the provisioning process in the <strong>Status</strong> column of your CLI output. If your worker node is stuck in this state for a long time, continue with the next step to see whether a problem occurred during the provisioning.</td>
    </tr>
    <tr>
      <td>`Provision_failed`</td>
      <td>Your worker node could not be provisioned. Continue with the next step to find the details for the failure.</td>
    </tr>
 <tr>
      <td>`Reloading`</td>
      <td>Your worker node is being reloaded and is not available in the cluster. You can monitor the reloading process in the <strong>Status</strong> column of your CLI output. If your worker node is stuck in this state for a long time, continue with the next step to see whether a problem occurred during the reloading.</td>
     </tr>
     <tr>
      <td>`Reloading_failed`</td>
      <td>Your worker node could not be reloaded. Continue with the next step to find the details for the failure.</td>
    </tr>
    <tr>
      <td>`Reload_pending`</td>
      <td>A request to reload or to update the Kubernetes version of your worker node is sent. When the worker node is being reloaded, the state changes to <code>Reloading</code>. </td>
    </tr>
    <tr>
     <td>`Unknown`</td>
     <td>The Kubernetes master is not reachable for one of the following reasons:<ul><li>You requested an update of your Kubernetes master. The state of the worker node cannot be retrieved during the update. If the worker node remains in this state for an extended period of time even after the Kubernetes master is successfully updated, try to [reload](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_worker_reload) the worker node.</li><li>You might have another firewall that is protecting your worker nodes, or changed firewall settings recently. {{site.data.keyword.containerlong_notm}} requires certain IP addresses and ports to be opened to allow communication from the worker node to the Kubernetes master and vice versa. For more information, see [Firewall prevents worker nodes from connecting](/docs/containers?topic=containers-cs_troubleshoot_clusters#cs_firewall).</li><li>The Kubernetes master is down. Contact {{site.data.keyword.cloud_notm}} support by opening an [{{site.data.keyword.cloud_notm}} support case](/docs/containers?topic=containers-cs_troubleshoot#ts_getting_help).</li></ul></td>
</tr>
   <tr>
      <td>`Warning`</td>
      <td>Your worker node is reaching the limit for memory or disk space. You can either reduce work load on your worker node or add a worker node to your cluster to help load balance the work load.</td>
</tr>
  </tbody>
</table>
</p></li>
<li>List the details for the worker node. If the details include an error message, review the list of [common error messages for worker nodes](#common_worker_nodes_issues) to learn how to resolve the problem.<p class="pre">ibmcloud ks worker-get --cluster <cluster_name_or_id> --worker <worker_node_id></p></li>
</ol>

<br />


## Common issues with worker nodes
{: #common_worker_nodes_issues}

Review common error messages and learn how to resolve them.

  <table>
  <caption>Common error messages</caption>
    <thead>
    <th>Error message</th>
    <th>Description and resolution
    </thead>
    <tbody>
      <tr>
        <td>{{site.data.keyword.cloud_notm}} Infrastructure Exception: Your account is currently prohibited from ordering 'Computing Instances'.</td>
        <td>Your IBM Cloud infrastructure account might be restricted from ordering compute resources. Contact {{site.data.keyword.cloud_notm}} support by opening an [{{site.data.keyword.cloud_notm}} support case](#ts_getting_help).</td>
      </tr>
      <tr>
      <td>{{site.data.keyword.cloud_notm}} infrastructure exception: Could not place order.<br><br>
      {{site.data.keyword.cloud_notm}} Infrastructure Exception: Could not place order. There are insufficient resources behind router 'router_name' to fulfill the request for the following guests: 'worker_id'.</td>
      <td>The zone that you selected might not have enough infrastructure capacity to provision your worker nodes. Or, you might have exceeded a limit in your IBM Cloud infrastructure account. To resolve, try one of the following options:
      <ul><li>Infrastructure resource availability in zones can fluctuate often. Wait a few minutes and try again.</li>
      <li>For a single zone cluster, create the cluster in a different zone. For a multizone cluster, add a zone to the cluster.</li>
      <li>Specify a different pair of public and private VLANs for your worker nodes in your IBM Cloud infrastructure account. For worker nodes that are in a worker pool, you can use the <code>ibmcloud ks zone-network-set</code> [command](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_zone_network_set).</li>
      <li>Contact your IBM Cloud infrastructure account manager to verify that you do not exceed an account limit, such as a global quota.</li>
      <li>Open an [IBM Cloud infrastructure support case](#ts_getting_help)</li></ul></td>
      </tr>
      <tr>
        <td>{{site.data.keyword.cloud_notm}} Infrastructure Exception: Could not obtain network VLAN with ID: <code>&lt;vlan id&gt;</code>.</td>
        <td>Your worker node could not be provisioned because the selected VLAN ID could not be found for one of the following reasons:<ul><li>You might have specified the VLAN number instead of the VLAN ID. The VLAN number is 3 or 4 digits long, whereas the VLAN ID is 7 digits long. Run <code>ibmcloud ks vlans --zone &lt;zone&gt;</code> to retrieve the VLAN ID.<li>The VLAN ID might not be associated with the IBM Cloud infrastructure account that you use. Run <code>ibmcloud ks vlans --zone &lt;zone&gt;</code> to list available VLAN IDs for your account. To change the IBM Cloud infrastructure account, see [`ibmcloud ks credential-set`](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_credentials_set). </ul></td>
      </tr>
      <tr>
        <td>SoftLayer_Exception_Order_InvalidLocation: The location provided for this order is invalid. (HTTP 500)</td>
        <td>Your IBM Cloud infrastructure is not set up to order compute resources in the selected data center. Contact [{{site.data.keyword.cloud_notm}} support](#ts_getting_help) to verify that you account is set up correctly.</td>
       </tr>
       <tr>
        <td>{{site.data.keyword.cloud_notm}} Infrastructure Exception: The user does not have the necessary {{site.data.keyword.cloud_notm}} Infrastructure permissions to add servers
        </br></br>
        {{site.data.keyword.cloud_notm}} Infrastructure Exception: 'Item' must be ordered with permission.
        </br></br>
        The {{site.data.keyword.cloud_notm}} infrastructure credentials could not be validated.</td>
        <td>You might not have the required permissions to perform the action in your IBM Cloud infrastructure portfolio, or you are using the wrong infrastructure credentials. See [Setting up the API key to enable access to the infrastructure portfolio](/docs/containers?topic=containers-users#api_key).</td>
      </tr>
      <tr>
       <td>Worker unable to talk to {{site.data.keyword.containerlong_notm}} servers. Please verify your firewall setup is allowing traffic from this worker.
       <td><ul><li>If you have a firewall, [configure your firewall settings to allow outgoing traffic to the appropriate ports and IP addresses](/docs/containers?topic=containers-firewall#firewall_outbound).</li>
       <li>Check whether your cluster does not have a public IP by running `ibmcloud ks workers --cluster <mycluster>`. If no public IP is listed, then your cluster has only private VLANs.
       <ul><li>If you want the cluster to have only private VLANs, set up your [VLAN connection](/docs/containers?topic=containers-plan_clusters#private_clusters) and your [firewall](/docs/containers?topic=containers-firewall#firewall_outbound).</li>
       <li>If you created the cluster with only the private service endpoint before you enabled your account for [VRF](/docs/infrastructure/direct-link?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud#overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud) and [service endpoints](/docs/resources?topic=resources-private-network-endpoints#getting-started), your workers cannot connect to the master. Try [setting up the public service endpoint](/docs/containers?topic=containers-cs_network_cluster#set-up-public-se) so that you can use your cluster until your support cases are processed to update your account. If you still want a private service endpoint only cluster after your account is updated, you can then disable the public service endpoint.</li>
       <li>If you want the cluster to have a public IP, [add new worker nodes](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_worker_add) with both public and private VLANs.</li></ul></li></ul></td>
     </tr>
      <tr>
  <td>Cannot create IMS portal token, as no IMS account is linked to the selected BSS account</br></br>Provided user not found or active</br></br>SoftLayer_Exception_User_Customer_InvalidUserStatus: User account is currently cancel_pending.</br></br>Waiting for machine to be visible to the user</td>
  <td>The owner of the API key that is used to access the IBM Cloud infrastructure portfolio does not have the required permissions to perform the action, or might be pending deletion.</br></br><strong>As the user</strong>, follow these steps:
  <ol><li>If you have access to multiple accounts, make sure that you are logged in to the account where you want to work with {{site.data.keyword.containerlong_notm}}. </li>
  <li>Run <code>ibmcloud ks api-key-info --cluster &lt;cluster_name_or_ID&gt;</code> to view the current API key owner that is used to access the IBM Cloud infrastructure portfolio. </li>
  <li>Run <code>ibmcloud account list</code> to view the owner of the {{site.data.keyword.cloud_notm}} account that you currently use. </li>
  <li>Contact the owner of the {{site.data.keyword.cloud_notm}} account and report that the API key owner has insufficient permissions in IBM Cloud infrastructure or might be pending to be deleted. </li></ol>
  </br><strong>As the account owner</strong>, follow these steps:
  <ol><li>Review the [required permissions in IBM Cloud infrastructure](/docs/containers?topic=containers-users#infra_access) to perform the action that previously failed. </li>
  <li>Fix the permissions of the API key owner or create a new API key by using the [<code>ibmcloud ks api-key-reset --region <region></code>](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_api_key_reset) command. </li>
  <li>If you or another account admin manually set IBM Cloud infrastructure credentials in your account, run [<code>ibmcloud ks credential-unset --region <region></code>](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_credentials_unset) to remove the credentials from your account.</li></ol></td>
  </tr>
    </tbody>
  </table>

<br />


## Reviewing master health
{: #debug_master}

Your {{site.data.keyword.containerlong_notm}} includes an IBM-managed master with highly available replicas, automatic security patch updates applied for you, and automation in place to recover in case of an incident. You can check the health, status, and state of the cluster master by running `ibmcloud ks cluster-get --cluster <cluster_name_or_ID>`.
{: shortdesc} 

**Master Health**<br>
The **Master Health** reflects the state of master components and notifies you if something needs your attention. The health might be one of the following:
*   `error`: The master is not operational. IBM is automatically notified and takes action to resolve this issue. You can continue monitoring the health until the master is `normal`.
*   `normal`: The master is operational and healthy. No action is required.
*   `unavailable`: The master might not be accessible, which means some actions such as resizing a worker pool are temporarily unavailable. IBM is automatically notified and takes action to resolve this issue. You can continue monitoring the health until the master is `normal`. 
*   `unsupported`: The master runs an unsupported version of Kubernetes. You must [update your cluster](/docs/containers?topic=containers-update) to return the master to `normal` health.

**Master Status and State**<br>
The **Master Status** provides details of what operation from the master state is in progress. The status includes a timestamp of how long the master has been in the same state, such as `Ready (1 month ago)`. The **Master State** reflects the lifecycle of possible operations that can be performed on the master, such as deploying, updating, and deleting. Each state is described in the following table.

<table summary="Every table row should be read left to right, with the master state in column one and a description in column two.">
<caption>Master states</caption>
   <thead>
   <th>Master state</th>
   <th>Description</th>
   </thead>
   <tbody>
<tr>
   <td>`deployed`</td>
   <td>The master is successfully deployed. Check the status to verify that the master is `Ready` or to see if an update is available.</td>
   </tr>
 <tr>
     <td>`deploying`</td>
     <td>The master is currently deploying. Wait for the state to become `deployed` before working with your cluster, such as adding worker nodes.</td>
    </tr>
   <tr>
     <td>`deploy_failed`</td>
     <td>The master failed to deploy. IBM Support is notified and works to resolve the issue. Check the **Master Status** field for more information, or wait for the state to become `deployed`.</td>
   </tr>
   <tr>
   <td>`deleting`</td>
   <td>The master is currently deleting because you deleted the cluster. You cannot undo a deletion. After the cluster is deleted, you can no longer check the master state because the cluster is completely removed.</td>
   </tr>
     <tr>
       <td>`delete_failed`</td>
       <td>The master failed to delete. IBM Support is notified and works to resolve the issue. You cannot resolve the issue by trying to delete the cluster again. Instead, check the **Master Status** field for more information, or wait for the cluster to delete.</td>
      </tr>
      <tr>
       <td>`updating`</td>
       <td>The master is updating its Kubernetes version. The update might be a patch update that is automatically applied, or a minor or major version that you applied by updating the cluster. During the update, your highly available master can continue processing requests, and your app workloads and worker nodes continue to run. After the master update is complete, you can [update your worker nodes](/docs/containers?topic=containers-update#worker_node).<br><br>
       If the update is unsuccessful, the master returns to a `deployed` state and continues running the previous version. IBM Support is notified and works to resolve the issue. You can check if the update failed in the **Master Status** field.</td>
    </tr>
   </tbody>
 </table>


<br />



## Debugging app deployments
{: #debug_apps}

Review the options that you have to debug your app deployments and find the root causes for failures.

Before you begin, ensure you have the [**Writer** or **Manager** {{site.data.keyword.cloud_notm}} IAM service role](/docs/containers?topic=containers-users#platform) for the namespace where your app is deployed.

1. Look for abnormalities in the service or deployment resources by running the `describe` command.

 Example:
 <pre class="pre"><code>kubectl describe service &lt;service_name&gt; </code></pre>

2. [Check whether the containers are stuck in the `ContainerCreating` state](/docs/containers?topic=containers-cs_troubleshoot_storage#stuck_creating_state).

3. Check whether the cluster is in the `Critical` state. If the cluster is in a `Critical` state, check the firewall rules and verify that the master can communicate with the worker nodes.

4. Verify that the service is listening on the correct port.
   1. Get the name of a pod.
     <pre class="pre"><code>kubectl get pods</code></pre>
   2. Log in to a container.
     <pre class="pre"><code>kubectl exec -it &lt;pod_name&gt; -- /bin/bash</code></pre>
   3. Curl the app from within the container. If the port is not accessible, the service might not be listening on the correct port or the app might have issues. Update the configuration file for the service with the correct port and redeploy or investigate potential issues with the app.
     <pre class="pre"><code>curl localhost: &lt;port&gt;</code></pre>

5. Verify that the service is linked correctly to the pods.
   1. Get the name of a pod.
     <pre class="pre"><code>kubectl get pods</code></pre>
   2. Log in to a container.
     <pre class="pre"><code>kubectl exec -it &lt;pod_name&gt; -- /bin/bash</code></pre>
   3. Curl the cluster IP address and port of the service. If the IP address and port are not accessible, look at the endpoints for the service. If no endpoints are listed, then the selector for the service does not match the pods. If endpoints are listed, then look at the target port field on the service and make sure that the target port is the same as what is being used for the pods.
     <pre class="pre"><code>curl &lt;cluster_IP&gt;:&lt;port&gt;</code></pre>

6. For Ingress services, verify that the service is accessible from within the cluster.
   1. Get the name of a pod.
     <pre class="pre"><code>kubectl get pods</code></pre>
   2. Log in to a container.
     <pre class="pre"><code>kubectl exec -it &lt;pod_name&gt; -- /bin/bash</code></pre>
   2. Curl the URL specified for the Ingress service. If the URL is not accessible, check for a firewall issue between the cluster and the external endpoint. 
     <pre class="pre"><code>curl &lt;host_name&gt;.&lt;domain&gt;</code></pre>

<br />



## Getting help and support
{: #ts_getting_help}

Still having issues with your cluster?
{: shortdesc}

-  In the terminal, you are notified when updates to the `ibmcloud` CLI and plug-ins are available. Be sure to keep your CLI up-to-date so that you can use all available commands and flags.
-   To see whether {{site.data.keyword.cloud_notm}} is available, [check the {{site.data.keyword.cloud_notm}} status page ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/status?selected=status).
-   Post a question in the [{{site.data.keyword.containerlong_notm}} Slack ![External link icon](../icons/launch-glyph.svg "External link icon")](https://ibm-container-service.slack.com).
    If you are not using an IBM ID for your {{site.data.keyword.cloud_notm}} account, [request an invitation](https://cloud.ibm.com/kubernetes/slack) to this Slack.
    {: tip}
-   Review the forums to see whether other users ran into the same issue. When you use the forums to ask a question, tag your question so that it is seen by the {{site.data.keyword.cloud_notm}} development teams.
    -   If you have technical questions about developing or deploying clusters or apps with {{site.data.keyword.containerlong_notm}}, post your question on [Stack Overflow ![External link icon](../icons/launch-glyph.svg "External link icon")](https://stackoverflow.com/questions/tagged/ibm-cloud+containers) and tag your question with `ibm-cloud`, `kubernetes`, and `containers`.
    -   For questions about the service and getting started instructions, use the [IBM Developer Answers ![External link icon](../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/answers/topics/containers/?smartspace=bluemix) forum. Include the `ibm-cloud` and `containers` tags.
    See [Getting help](/docs/get-support?topic=get-support-getting-customer-support#using-avatar) for more details about using the forums.
-   Contact IBM Support by opening a case. To learn about opening an IBM support case, or about support levels and case severities, see [Contacting support](/docs/get-support?topic=get-support-getting-customer-support).
When you report an issue, include your cluster ID. To get your cluster ID, run `ibmcloud ks clusters`. You can also use the [{{site.data.keyword.containerlong_notm}} Diagnostics and Debug Tool](/docs/containers?topic=containers-cs_troubleshoot#debug_utility) to gather and export pertinent information from your cluster to share with IBM Support.
{: tip}

