---

copyright:
  years: 2014, 2020
lastupdated: "2020-06-23"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift

---

{:beta: .beta}
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



# Worker nodes
{: #cs_troubleshoot_clusters}

As you use Red Hat OpenShift on IBM Cloud, consider these techniques for general troubleshooting and debugging your cluster and cluster master.
{: shortdesc}

**General ways to resolve issues**<br>
1. Keep your cluster environment up to date.
   * Check monthly for available security and operating system patches to [update your worker nodes](/docs/openshift?topic=openshift-update#worker_node).
   * [Update your cluster](/docs/openshift?topic=openshift-update#master) to the latest default version for [OpenShift](/docs/containers?topic=containers-cs_versions).
2. Make sure that your command line tools are up to date.
   * In the terminal, you are notified when updates to the `ibmcloud` CLI and plug-ins are available. Be sure to keep your CLI up-to-date so that you can use all available commands and flags.
   * Make sure that [your `oc` CLI](/docs/openshift?topic=openshift-openshift-cli#cli_oc) client matches the same Kubernetes version as your cluster server. [Kubernetes does not support](https://kubernetes.io/docs/setup/release/version-skew-policy/){: external} `oc` client versions that are 2 or more versions apart from the server version (n +/- 2).
<br>

**Reviewing issues and status**<br>
1. To see whether {{site.data.keyword.cloud_notm}} is available, [check the {{site.data.keyword.cloud_notm}} status page](https://cloud.ibm.com/status?selected=status){: external}.
2. Filter for the **Kubernetes Service** component.

## Debugging worker nodes
{: #debug_worker_nodes}
{: troubleshoot}
{: support}

Review the options to debug your worker nodes and find the root causes for failures.

1. If your cluster is in a **Critical**, **Delete failed**, or **Warning** state, or is stuck in the **Pending** state for a long time, review the state of your worker nodes.
    ```
    ibmcloud oc worker ls --cluster <cluster_name_or_id>
    ```
    {: pre}
2. Review the **State** and **Status** field for every worker node in your CLI output.
    You can view the current worker node state by running the `ibmcloud oc worker ls --cluster <cluster_name_or_ID` command and locating the **State** and **Status** fields.
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
        <li>The pods that are deployed to your worker node do not use proper resource limits for [memory](https://kubernetes.io/docs/tasks/configure-pod-container/assign-memory-resource/){: external} and [CPU](https://kubernetes.io/docs/tasks/configure-pod-container/assign-cpu-resource/){: external}. If you set none or excessive resource limits, pods can consume all available resources, leaving no resources for other pods to run on this worker node. This overcommitment of workload causes the worker node to fail. <ol><li>List the pods that run on your worker node and review the CPU and memory usage, requests and limits. <pre class="codeblock"><code>oc describe node &lt;worker_private_IP&gt;</code></pre></li><li>For pods that consume a lot of memory and CPU resources, check if you set proper resource limits for memory and CPU. <pre class="codeblock"><code>oc get pods &lt;pod_name&gt; -n &lt;namespace&gt; -o json</code></pre></li><li>Optional: Remove the resource-intensive pods to free up compute resources on your worker node. <pre class="codeblock"><code>oc delete pod &lt;pod_name&gt;</code></pre><pre class="codeblock"><code>oc delete deployment &lt;deployment_name&gt;</code></pre></li></ol></li>
        <li><code>containerd</code>, <code>kubelet</code>, or <code>calico</code> went into an unrecoverable state after it ran hundreds or thousands of containers over time. </li>
        <li>You set up a Virtual Router Appliance for your worker node that went down and cut off the communication between your worker node and the Kubernetes master. </li><li> Current networking issues in {{site.data.keyword.containerlong_notm}} or IBM Cloud infrastructure that causes the communication between your worker node and the Kubernetes master to fail.</li>
        <li>Your worker node ran out of capacity. Check the <strong>Status</strong> of the worker node to see whether it shows <strong>Out of disk</strong> or <strong>Out of memory</strong>. If your worker node is out of capacity, consider to either reduce the workload on your worker node or add a worker node to your cluster to help load balance the workload.</li>
        <li>The device was powered off from the [{{site.data.keyword.cloud_notm}} console resource list ![External link icon](../icons/launch-glyph.svg "External link icon")](https://cloud.ibm.com/resources). Open the resource list and find your worker node ID in the **Devices** list. In the action menu, click **Power On**.</li></ul>
        In many cases, [reloading](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reload) your worker node can solve the problem. When you reload your worker node, the latest [patch version](/docs/containers?topic=containers-cs_versions#version_types) is applied to your worker node. The major and minor version is not changed. Before you reload your worker node, make sure to cordon and drain your worker node to ensure that the existing pods are terminated gracefully and rescheduled onto remaining worker nodes. </br></br> If reloading the worker node does not resolve the issue, go to the next step to continue troubleshooting your worker node.
        </td>
       </tr>
       <tr>
       <td>`Deployed`</td>
       <td>Updates are successfully deployed to your worker node. After updates are deployed, Red Hat OpenShift on IBM Cloud starts a health check on the worker node. After the health check is successful, the worker node goes into a <code>Normal</code> state. Worker nodes in a <code>Deployed</code> state usually are ready to receive workloads, which you can check by running <code>oc get nodes</code> and confirming that the state shows <code>Normal</code>. </td>
       </tr>
        <tr>
          <td>`Deploying`</td>
          <td>When you update the Kubernetes version of your worker node, your worker node is redeployed to install the updates. If you reload or reboot your worker node, the worker node is redeployed to automatically install the latest patch version. If your worker node is stuck in this state for a long time, continue with the next step to see whether a problem occurred during the deployment. </td>
       </tr>
       <tr>
         <td>`Deploy_failed`</td>
         <td>Your worker node could not be deployed. List the details for the worker node to find the details for the failure by running `ibmcloud oc worker get --cluster <cluster_name_or_id> --worker <worker_node_id>`.</td>
       </tr>
          <tr>
          <td>`Normal`</td>
          <td>Your worker node is fully provisioned and ready to be used in the cluster. This state is considered healthy and does not require an action from the user. **Note**: Although the worker nodes might be normal, other infrastructure resources, such as [networking](/docs/openshift?topic=openshift-cs_troubleshoot_network) and [storage](/docs/openshift?topic=openshift-cs_troubleshoot_storage), might still need attention.</td>
       </tr>
     <tr>
          <td>`Provisioning`</td>
          <td>Your worker node is being provisioned and is not available in the cluster yet. You can monitor the provisioning process in the <strong>Status</strong> column of your CLI output. If your worker node is stuck in this state for a long time, continue with the next step to see whether a problem occurred during the provisioning.</td>
        </tr>
        <tr>
          <td>`Provision_failed`</td>
          <td>Your worker node could not be provisioned. List the details for the worker node to find the details for the failure by running `ibmcloud oc worker get --cluster <cluster_name_or_id> --worker <worker_node_id>`.</td>
        </tr>
     <tr>
          <td>`Reloading`</td>
          <td>Your worker node is being reloaded and is not available in the cluster. You can monitor the reloading process in the <strong>Status</strong> column of your CLI output. If your worker node is stuck in this state for a long time, continue with the next step to see whether a problem occurred during the reloading.</td>
         </tr>
         <tr>
          <td>`Reloading_failed`</td>
          <td>Your worker node could not be reloaded. List the details for the worker node to find the details for the failure by running `ibmcloud oc worker get --cluster <cluster_name_or_id> --worker <worker_node_id>`.</td>
        </tr>
        <tr>
          <td>`Reload_pending`</td>
          <td>A request to reload or to update the Kubernetes version of your worker node is sent. When the worker node is being reloaded, the state changes to <code>Reloading</code>. </td>
        </tr>
        <tr>
         <td>`Unknown`</td>
         <td>The Kubernetes master is not reachable for one of the following reasons:<ul><li>You requested an update of your Kubernetes master. The state of the worker node cannot be retrieved during the update. If the worker node remains in this state for an extended period of time even after the Kubernetes master is successfully updated, try to [reload](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reload) the worker node.</li><li>You might have another firewall that is protecting your worker nodes, or changed firewall settings recently. Red Hat OpenShift on IBM Cloud requires certain IP addresses and ports to be opened to allow communication from the worker node to the Kubernetes master and vice versa. For more information, see [Firewall prevents worker nodes from connecting](/docs/openshift?topic=openshift-firewall#vyatta_firewall).</li><li>The Kubernetes master is down. Contact {{site.data.keyword.cloud_notm}} support by opening an [{{site.data.keyword.cloud_notm}} support case](/docs/openshift?topic=openshift-cs_troubleshoot#getting_help).</li></ul></td>
    </tr>
       <tr>
          <td>`Warning`</td>
          <td>Your worker node is reaching the limit for memory or disk space. You can either reduce work load on your worker node or add a worker node to your cluster to help load balance the work load.</td>
    </tr>
      </tbody>
    </table>

3. List the details for the worker node. If the details include an error message, review the list of [common error messages for worker nodes](#common_worker_nodes_issues) to learn how to resolve the problem.
    ```
    ibmcloud oc worker get --cluster <cluster_name_or_id> --worker <worker_node_id>
    ```
    {: pre}

<br />


## Common issues with worker nodes
{: #common_worker_nodes_issues}

Review common error messages and learn how to resolve them. Messages might begin with the prefix, `'<provider>' infrastructure exception:`, where `<provider>` identifies which infrastructure provider the worker node uses.
{: shortdesc}

  <table>
  <caption>Common error messages</caption>
    <col width="25%">
    <thead>
    <th>Error message</th>
    <th>Description and resolution
    </thead>
    <tbody>
      <tr>
        <td>Your account is currently prohibited from ordering 'Computing Instances'.</td>
        <td>Your IBM Cloud infrastructure account might be restricted from ordering compute resources. Contact {{site.data.keyword.cloud_notm}} support by opening an [{{site.data.keyword.cloud_notm}} support case](#getting_help_workers).</td>
      </tr>
      <tr>
      <td>Could not place order.<br><br>
      Could not place order. There are insufficient resources behind router 'router_name' to fulfill the request for the following guests: 'worker_id'.</td>
      <td>The zone that you selected might not have enough infrastructure capacity to provision your worker nodes. Or you might have exceeded a limit in your IBM Cloud infrastructure account. To resolve, try one of the following options:
      <ul><li>Infrastructure resource availability in zones can fluctuate often. Wait a few minutes and try again.</li>
      <li>For a single zone cluster, create the cluster in a different zone. For a multizone cluster, add a zone to the cluster.</li>
      <li>Specify a different pair of public and private VLANs for your worker nodes in your IBM Cloud infrastructure account. For worker nodes that are in a worker pool, you can use the <code>ibmcloud oc zone network-set</code> [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_zone_network_set).</li>
      <li>Contact your IBM Cloud infrastructure account manager to verify that you do not exceed an account limit, such as a global quota.</li>
      <li>Open an [IBM Cloud infrastructure support case](#getting_help_workers)</li></ul></td>
      </tr>
      <tr>
        <td>Could not obtain network VLAN with ID: <code>&lt;vlan id&gt;</code>.</td>
        <td>Your worker node could not be provisioned because the selected VLAN ID could not be found for one of the following reasons:<ul><li>You might have specified the VLAN number instead of the VLAN ID. The VLAN number is 3 or 4 digits long, whereas the VLAN ID is 7 digits long. Run <code>ibmcloud oc vlan ls --zone &lt;zone&gt;</code> to retrieve the VLAN ID.<li>The VLAN ID might not be associated with the IBM Cloud infrastructure account that you use. Run <code>ibmcloud oc vlan ls --zone &lt;zone&gt;</code> to list available VLAN IDs for your account. To change the IBM Cloud infrastructure account, see [`ibmcloud oc credential set`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_credentials_set). </ul></td>
      </tr>
      <tr>
        <td>The location provided for this order is invalid.</td>
        <td>Your IBM Cloud infrastructure is not set up to order compute resources in the selected data center. Contact [{{site.data.keyword.cloud_notm}} support](#getting_help_workers) to verify that you account is set up correctly.</td>
       </tr>
       <tr>
        <td>The user does not have the necessary {{site.data.keyword.cloud_notm}} classic infrastructure permissions to add servers
        </br></br>
        'Item' must be ordered with permission.
        </br></br>
        The IBM Cloud infrastructure credentials could not be validated.<br><br>
        '<Provider>' infrastructure request not authorized</td>
        <td>You might not have the required permissions to perform the action in your IBM Cloud infrastructure portfolio, or you are using the wrong infrastructure credentials. See [Setting up the API key to enable access to the infrastructure portfolio](/docs/openshift?topic=openshift-users#api_key).</td>
      </tr>
      <tr>
       <td>Worker unable to talk to {{site.data.keyword.containerlong_notm}} servers. Please verify your firewall setup is allowing traffic from this worker.
       <td><ul><li>If you have a firewall, [configure your firewall settings to allow outgoing traffic to the appropriate ports and IP addresses](/docs/openshift?topic=openshift-firewall#firewall_outbound).</li></ul></td>
     </tr>
  <tr>
    <td>The worker did not respond to the soft reboot request. A hard reboot might be necessary.</td>
    <td>Although you issued a reboot on your worker node, the worker node is unresponsive. You can rerun the [reboot command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reboot) with the `--hard` flag to power off the worker node, or run the `worker reload` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reload).</td>
  </tr>
      <tr>
  <td>Cannot create IMS portal token, as no IMS account is linked to the selected BSS account</br></br>Provided user not found or active</br></br>User account is currently cancel_pending.</br></br>The worker node instance '&lt;ID&gt;' cannot be found. Review '&lt;provider&gt;' infrastructure user permissions.<br><br>The worker node instance cannot be found. Review '&lt;provider&gt;' infrastructure user permissions.<br><br>The worker node instance cannot be identified. Review '&lt;provider&gt;' infrastructure user permissions.</td>
  <td>The owner of the API key that is used to access the IBM Cloud infrastructure portfolio does not have the required permissions to perform the action, or might be pending deletion.</br></br><strong>As the user</strong>, follow these steps:
  <ol><li>If you have access to multiple accounts, make sure that you are logged in to the account where you want to work with Red Hat OpenShift on IBM Cloud. </li>
  <li>Run <code>ibmcloud oc api-key info --cluster &lt;cluster_name_or_ID&gt;</code> to view the current API key owner that is used to access the IBM Cloud infrastructure portfolio. </li>
  <li>Run <code>ibmcloud account list</code> to view the owner of the {{site.data.keyword.cloud_notm}} account that you currently use. </li>
  <li>Contact the owner of the {{site.data.keyword.cloud_notm}} account and report that the API key owner has insufficient permissions in IBM Cloud infrastructure or might be pending to be deleted. </li></ol>
  </br><strong>As the account owner</strong>, follow these steps:
  <ol><li>Review the [required classic permissions in IBM Cloud infrastructure](/docs/openshift?topic=openshift-users#infra_access) to perform the action that previously failed. For the VPC infrastructure provider, the API key owner must have the **Administrator** platform role.</li>
  <li>Fix the permissions of the API key owner or create a new API key by using the [<code>ibmcloud oc api-key reset --region <region></code>](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_api_key_reset) command. </li>
  <li>If you or another account admin manually set IBM Cloud infrastructure credentials in your account, run [<code>ibmcloud oc credential unset --region <region></code>](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_credentials_unset) to remove the credentials from your account.</li></ol></td>
  </tr>
    </tbody>
  </table>

<br />


## Unable to create a cluster or manage worker nodes due to permission errors
{: #cs_credentials}
{: troubleshoot}
{: support}

{: tsSymptoms}
You try to manage worker nodes for a new or an existing cluster by running one of the following commands.
* Provision workers: `ibmcloud oc cluster create classic`, `ibmcloud oc worker-pool rebalance`, or `ibmcloud oc worker-pool resize`
* Reload workers: `ibmcloud oc worker reload` or `ibmcloud oc worker update`
* Reboot workers: `ibmcloud oc worker reboot`
* Delete workers: `ibmcloud oc cluster rm`, `ibmcloud oc worker rm`, `ibmcloud oc worker-pool rebalance`, or `ibmcloud oc worker-pool resize`

However, you receive an error message similar to one of the following.

```
We were unable to connect to your IBM Cloud infrastructure account.
Creating a standard cluster requires that you have either a
Pay-As-You-Go account that is linked to an IBM Cloud infrastructure
account term or that you have used the {{site.data.keyword.containerlong_notm}}
CLI to set your {{site.data.keyword.cloud_notm}} Infrastructure API keys.
```
{: screen}

```
'Item' must be ordered with permission.
```
{: screen}

```
The worker node instance '<ID>' cannot be found. Review '<provider>' infrastructure user permissions.
```
{: screen}

```
The worker node instance cannot be found. Review '<provider>' infrastructure user permissions.
```
{: screen}

```
The worker node instance cannot be identified. Review '<provider>' infrastructure user permissions.
```
{: screen}

```
The IAM token exchange request failed with the message: <message>
IAM token exchange request failed: <message>
```
{: screen}

```
The cluster could not be configured with the registry. Make sure that you have the Administrator role for {{site.data.keyword.registrylong_notm}}.
```
{: screen}

{: tsCauses}
The infrastructure credentials that are set for the region and resource group are missing the appropriate [infrastructure permissions](/docs/openshift?topic=openshift-access_reference#infra). The user's infrastructure permissions are most commonly stored as an [API key](/docs/openshift?topic=openshift-users#api_key) for the region and resource group. More rarely, if you use a [different {{site.data.keyword.cloud_notm}} account type](/docs/openshift?topic=openshift-users#understand_infra), you might have [set infrastructure credentials manually](/docs/openshift?topic=openshift-users#credentials). If you use a different classic IBM Cloud infrastructure account to provision infrastructure resources, you might also have [orphaned clusters](/docs/openshift?topic=openshift-cs_troubleshoot_clusters#orphaned) in your account.

{: tsResolve}
The account owner must set up the infrastructure account credentials properly. The credentials depend on what type of infrastructure account you are using.

Before you begin, [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/openshift?topic=openshift-cs_cli_install#cs_cli_configure).

1.  Identify what user credentials are used for the region and resource group's infrastructure permissions.
    1.  Check the API key for a region and resource group of the cluster.
        ```
        ibmcloud oc api-key info --cluster <cluster_name_or_ID>
        ```
        {: pre}

        Example output:
        ```
        Getting information about the API key owner for cluster <cluster_name>...
        OK
        Name                Email
        <user_name>         <name@email.com>
        ```
        {: screen}
    2.  Check if the classic infrastructure account for the region and resource group is manually set to use a different IBM Cloud infrastructure account.
        ```
        ibmcloud oc credential get --region <us-south>
        ```
        {: pre}

        **Example output if credentials are set to use a different classic account**. In this case, the user's infrastructure credentials are used for the region and resource group that you targeted, even if a different user's credentials are stored in the API key that you retrieved in the previous step.
        ```
        OK
        Infrastructure credentials for user name <1234567_name@email.com> set for resource group <resource_group_name>.
        ```
        {: screen}

        **Example output if credentials are not set to use a different classic account**. In this case, the API key owner that you retrieved in the previous step has the infrastructure credentials that are used for the region and resource group.
        ```
        FAILED
        No credentials set for resource group <resource_group_name>.: The user credentials could not be found. (E0051)
        ```
        {: screen}
2.  Validate the infrastructure permissions that the user has.
    1.  List the suggested and required infrastructure permissions for the region and resource group.
        ```
        ibmcloud oc infra-permissions get --region <region>
        ```
        {: pre}

        For console and CLI commands to assign these permissions, see [Classic infrastructure roles](/docs/openshift?topic=openshift-access_reference#infra).
        {: tip}
    2.  Make sure that the [infrastructure credentials owner for the API key or the manually-set account has the correct permissions](/docs/openshift?topic=openshift-users#owner_permissions).
    3.  If necessary, you can change the [API key](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_api_key_reset) or [manually-set](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_credentials_set) infrastructure credentials owner for the region and resource group.
3.  Test that the changed permissions permit authorized users to perform infrastructure operations for the cluster.
    1.  For example, you might try to a delete a worker node.
        ```
        ibmcloud oc worker rm --cluster <cluster_name_or_ID> --worker <worker_node_ID>
        ```
        {: pre}
    2.  Check to see if the worker node is removed.
        ```
        ibmcloud oc worker get --cluster <cluster_name_or_ID> --worker <worker_node_ID>
        ```
        {: pre}

        Example output if the worker node removal is successful. The `worker get` operation fails because the worker node is deleted. The infrastructure permissions are correctly set up.
        ```
        FAILED
        The specified worker node could not be found. (E0011)
        ```
        {: screen}

    3.  If the worker node is not removed, review that [**State** and **Status** fields](/docs/openshift?topic=openshift-cs_troubleshoot_clusters#debug_worker_nodes) and the [common issues with worker nodes](/docs/openshift?topic=openshift-cs_troubleshoot_clusters#common_worker_nodes_issues) to continue debugging.
    4.  If you manually set credentials and still cannot see the cluster's worker nodes in your infrastructure account, you might check whether the [cluster is orphaned](/docs/openshift?topic=openshift-cs_troubleshoot_clusters#orphaned).

<br />


## Unable to create a cluster or manage worker nodes due to paid account error
{: #cs_totp}

{: tsSymptoms}
You try to manage worker nodes for a new or an existing cluster by running one of the following commands.
* Provision clusters and workers: `ibmcloud oc cluster create classic`, `ibmcloud oc worker-pool rebalance`, or `ibmcloud oc worker-pool resize`
* Reload workers: `ibmcloud oc worker reload` or `ibmcloud oc worker update`
* Reboot workers: `ibmcloud oc worker reboot`
* Delete clusters and workers: `ibmcloud oc cluster rm`, `ibmcloud oc worker rm`, `ibmcloud oc worker-pool rebalance`, or `ibmcloud oc worker-pool resize`

However, you receive an error message similar to the following.
```
Unable to connect to the IBM Cloud account. Ensure that you have a paid account.
```
{: screen}

{: tsCauses}
Your {{site.data.keyword.cloud_notm}} account uses its own automatically linked infrastructure through a Pay-as-you-Go account. However, the account administrator enabled the time-based one-time passcode (TOTP) option so that users are prompted for a time-based one-time passcode (TOTP) at login. This type of [multifactor authentication (MFA)](/docs/iam?topic=iam-types#account-based) is account-based, and affects all access to the account. TOTP MFA also affects the access that {{site.data.keyword.containerlong_notm}} requires to make calls to {{site.data.keyword.cloud_notm}} infrastructure. If TOTP is enabled for the account, you cannot create and manage clusters and worker nodes in {{site.data.keyword.containerlong_notm}}.

{: tsResolve}
Classic clusters only: The {{site.data.keyword.cloud_notm}} account owner or an account administrator must either:
* Disable TOTP for the account, and continue to use the automatically linked infrastructure credentials for {{site.data.keyword.containerlong_notm}}.
* Continue to use TOTP, but create an infrastructure API key that {{site.data.keyword.containerlong_notm}} can use to make direct calls to the {{site.data.keyword.cloud_notm}} infrastructure API.
**Note**: You cannot use TOTP if you want to use VPC clusters, because {{site.data.keyword.containerlong_notm}} does not support manually setting infrastructure credentials for VPC clusters.

**To disable TOTP MFA for the account:**
1. Log in to the [{{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/){: external}. From the menu bar, select **Manage > Access (IAM)**.
2. In the left navigation, click the **Settings** page.
3. Under **Multifactor authentication**, click **Edit**.
4. Select **None**, and click **Update**.

**To use TOTP MFA and create an infrastructure API key for {{site.data.keyword.containerlong_notm}}:**
1. From the [{{site.data.keyword.cloud_notm}}](https://cloud.ibm.com/){: external} console, select **Manage** > **Access (IAM)** > **Users** and click the name of the account owner. **Note**: If you do not use the account owner's credentials, first [ensure that the user whose credentials you use has the correct permissions](/docs/openshift?topic=openshift-users#owner_permissions).
2. In the **API Keys** section, find or create a classic infrastructure API key.
3. Use the infrastructure API key to set the infrastructure API credentials for {{site.data.keyword.containerlong_notm}}. Repeat this command for each region where you create clusters.
    ```
    ibmcloud oc credential set classic --infrastructure-username <infrastructure_API_username> --infrastructure-api-key <infrastructure_API_authentication_key> --region <region>
    ```
    {: pre}
4. Verify that the correct credentials are set.
    ```
    ibmcloud oc credential get --region <region>
    ```
    Example output:
    ```
    Infrastructure credentials for user name user@email.com set for resource group default.
    ```
    {: screen}
5. To ensure that existing clusters use the updated infrastructure API credentials, run `ibmcloud oc api-key reset --region <region>` in each region where you have clusters.

<br />



## Cannot add worker nodes due to an invalid VLAN ID
{: #suspended}

{: tsSymptoms}
Your {{site.data.keyword.cloud_notm}} account was suspended, or all worker nodes in your cluster were deleted. After the account is reactivated, you cannot add worker nodes when you try to resize or rebalance your worker pool. You see an error message similar to the following:

```
SoftLayerAPIError(SoftLayer_Exception_Public): Could not obtain network VLAN with id #123456.
```
{: screen}

{: tsCauses}
When an account is suspended, the worker nodes within the account are deleted. If a cluster has no worker nodes, IBM Cloud infrastructure reclaims the associated public and private VLANs. However, the cluster worker pool still has the previous VLAN IDs in its metadata and uses these unavailable IDs when you rebalance or resize the pool. The nodes fail to create because the VLANs are no longer associated with the cluster.

{: tsResolve}

You can [delete your existing worker pool](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_pool_rm), then [create a new worker pool](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_pool_create).

Alternatively, you can keep your existing worker pool by ordering new VLANs and using these to create new worker nodes in the pool.

Before you begin: [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/openshift?topic=openshift-cs_cli_install#cs_cli_configure)

1.  To get the zones that you need new VLAN IDs for, note the **Location** in the following command output. **Note**: If your cluster is a multizone, you need VLAN IDs for each zone.

    ```
    ibmcloud oc cluster ls
    ```
    {: pre}

2.  Get a new private and public VLAN for each zone that your cluster is in by [contacting {{site.data.keyword.cloud_notm}} support](/docs/vlans?topic=vlans-ordering-premium-vlans#ordering-premium-vlans).

3.  Note the new private and public VLAN IDs for each zone.

4.  Note the name of your worker pools.

    ```
    ibmcloud oc worker-pool ls --cluster <cluster_name_or_ID>
    ```
    {: pre}

5.  Use the `zone network-set` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_zone_network_set) to change the worker pool network metadata.

    ```
    ibmcloud oc zone network-set --zone <zone> --cluster <cluster_name_or_ID> -- worker-pool ls <worker-pool> --private-vlan <private_vlan_ID> --public-vlan <public_vlan_ID>
    ```
    {: pre}

6.  **Multizone cluster only**: Repeat **Step 5** for each zone in your cluster.

7.  Rebalance or resize your worker pool to add worker nodes that use the new VLAN IDs. For example:

    ```
    ibmcloud oc worker-pool resize --cluster <cluster_name_or_ID> --worker-pool <worker_pool> --size-per-zone <number_of_workers_per_zone>
    ```
    {: pre}

8.  Verify that your worker nodes are created.

    ```
    ibmcloud oc worker ls --cluster <cluster_name_or_ID> --worker-pool <worker_pool>
    ```
    {: pre}

<br />


## Unable to modify or delete infrastructure in an orphaned cluster
{: #orphaned}

{: tsSymptoms}
You cannot perform infrastructure-related commands on your cluster, such as:
* Adding or removing worker nodes
* Reloading or rebooting worker nodes
* Resizing worker pools
* Updating your cluster

You cannot view the cluster worker nodes in your classic IBM Cloud infrastructure account. However, you can update and manage other clusters in the account.

Further, you verified that you have the [proper infrastructure credentials](#cs_credentials).

{: tsCauses}
The cluster might be provisioned in a classic IBM Cloud infrastructure account that is no longer linked to your Red Hat OpenShift on IBM Cloud account. The cluster is orphaned. Because the resources are in a different account, you do not have the infrastructure credentials to modify the resources.

Consider the following scenario to understand how clusters might become orphaned.
1.  You have an {{site.data.keyword.cloud_notm}} Pay-As-You-Go account.
2.  You create a cluster named `Cluster1`. The worker nodes and other infrastructure resources are provisioned into the infrastructure account that comes with your Pay-As-You-Go account.
3.  Later, you find out that your team uses a legacy or shared classic IBM Cloud infrastructure account. You use the `ibmcloud oc credential set` command to change the IBM Cloud infrastructure credentials to use your team account.
4.  You create another cluster named `Cluster2`. The worker nodes and other infrastructure resources are provisioned into the team infrastructure account.
5.  You notice that `Cluster1` needs a worker node update, a worker node reload, or you just want to clean it up by deleting it. However, because `Cluster1` was provisioned into a different infrastructure account, you cannot modify its infrastructure resources. `Cluster1` is orphaned.
6.  You follow the resolution steps in the following section, but do not set your infrastructure credentials back to your team account. You can delete `Cluster1`, but now `Cluster2` is orphaned.
7.  You change your infrastructure credentials back to the team account that created `Cluster2`. Now, you no longer have an orphaned cluster!

<br>

{: tsResolve}
1.  Check which infrastructure account the region that your cluster is in currently uses to provision clusters.
    1.  Log in to the [Red Hat OpenShift on IBM Cloud clusters console](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}.
    2.  From the table, select your cluster.
    3.  In the **Overview** tab, check for an **Infrastructure User** field. This field helps you determine if your Red Hat OpenShift on IBM Cloud account uses a different infrastructure account than the default.
        * If you do not see the **Infrastructure User** field, you have a linked Pay-As-You-Go account that uses the same credentials for your infrastructure and platform accounts. The cluster that cannot be modified might be provisioned in a different infrastructure account.
        * If you see an **Infrastructure User** field, you use a different infrastructure account than the one that came with your Pay-As-You-Go account. These different credentials apply to all clusters within the region. The cluster that cannot be modified might be provisioned in your Pay-As-You-Go or a different infrastructure account.
2.  Check which infrastructure account was used to provision the cluster.
    1.  In the **Worker Nodes** tab, select a worker node and note its **ID**.
    2.  Open the menu ![Menu icon](../icons/icon_hamburger.svg "Menu icon") and click **Classic Infrastructure**.
    3.  From the infrastructure navigation pane, click **Devices > Device List**.
    4.  Search for the worker node ID that you previously noted.
    5.  If you do not find the worker node ID, the worker node is not provisioned into this infrastructure account. Switch to a different infrastructure account and try again.
3.  Use the `ibmcloud oc credential set` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_credentials_set) to change your infrastructure credentials to the account that the cluster worker nodes are provisioned in, which you found in the previous step.
    If you no longer have access to and cannot get the infrastructure credentials, you must open an {{site.data.keyword.cloud_notm}} support case to remove the orphaned cluster.
    {: note}
4.  [Delete the cluster](/docs/openshift?topic=openshift-remove).
5.  If you want, reset the infrastructure credentials to the previous account. Note that if you created clusters with a different infrastructure account than the account that you switch to, you might orphan those clusters.
    * To set credentials to a different infrastructure account, use the `ibmcloud oc credential set` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_credentials_set).
    * To use the default credentials that come with your {{site.data.keyword.cloud_notm}} Pay-As-You-Go account, use the `ibmcloud oc credential unset --region <region>` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_credentials_unset).

<br />


## Accessing your worker node with SSH fails
{: #cs_ssh_worker}

{: tsSymptoms}
You cannot access your worker node by using an SSH connection.

{: tsCauses}
SSH by password is unavailable on the worker nodes.

{: tsResolve}
Use a Kubernetes [`DaemonSet`](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/){: external} for actions that you must run on every node, or use jobs for one-time actions that you must run.

<br />


## Bare metal instance ID is inconsistent with worker records
{: #bm_machine_id}

{: tsSymptoms}
When you use `ibmcloud oc worker` commands with your bare metal worker node, you see a message similar to the following.

```
The worker node instance ID changed. Reload the worker node if bare metal hardware was serviced.
```
{: screen}

{: tsCauses}
The machine ID can become inconsistent with the Red Hat OpenShift on IBM Cloud worker record when the machine experiences hardware issues. When IBM Cloud infrastructure resolves this issue, a component can change within the system that the service does not identify.

{: tsResolve}
For Red Hat OpenShift on IBM Cloud to re-identify the machine, [reload the bare metal worker node](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reload). **Note**: Reloading also updates the machine's [patch version](/docs/containers?topic=containers-changelog).

You can also [delete the bare metal worker node](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_rm). **Note**: Bare metal instances are billed monthly.

<br />


## After a worker node updates or reloads, duplicate nodes and pods appear
{: #cs_duplicate_nodes}

{: tsSymptoms}
When you run `oc get nodes`, you see duplicate worker nodes with the status **`NotReady`**. The worker nodes with **`NotReady`** have public IP addresses, while the worker nodes with **`Ready`** have private IP addresses.

{: tsCauses}
Older clusters listed worker nodes by the cluster's public IP address. Now, worker nodes are listed by the cluster's private IP address. When you reload or update a node, the IP address is changed, but the reference to the public IP address remains.

{: tsResolve}
Service is not disrupted due to these duplicates, but you can remove the old worker node references from the API server.

  ```
  oc delete node <node_name1> <node_name2>
  ```
  {: pre}

<br />


## Accessing a pod on a new worker node fails with a timeout
{: #cs_nodes_duplicate_ip}

{: tsSymptoms}
You deleted a worker node in your cluster and then added a worker node. When you deployed a pod or Kubernetes service, the resource cannot access the newly created worker node, and the connection times out.

{: tsCauses}
If you delete a worker node from your cluster and then add a worker node, the new worker node might be assigned the private IP address of the deleted worker node. Calico uses this private IP address as a tag and continues to try to reach the deleted node.

{: tsResolve}
Manually update the reference of the private IP address to point to the correct node.

1.  Confirm that you have two worker nodes with the same **Private IP** address. Note the **Private IP** and **ID** of the deleted worker.

  ```
  ibmcloud oc worker ls --cluster <cluster_name_or_id>
  ```
  {: pre}

  ```
  ID                                                 Public IP       Private IP       Machine Type   State     Status   Zone   Version
  kube-dal10-cr9b7371a7fcbe46d08e04f046d5e6d8b4-w1   169.xx.xxx.xxx  10.xxx.xx.xxx    b3c.4x16       normal    Ready    dal10      1.17.7
  kube-dal10-cr9b7371a7fcbe46d08e04f046d5e6d8b4-w2   169.xx.xxx.xxx  10.xxx.xx.xxx    b3c.4x16       deleted    -       dal10      1.17.7
  ```
  {: screen}

2.  Install the [Calico CLI](/docs/openshift?topic=openshift-network_policies#adding_network_policies).
3.  List the available worker nodes in Calico. Replace <path_to_file> with the local path to the Calico configuration file.

  ```
  calicoctl get nodes --config=filepath/calicoctl.cfg
  ```
  {: pre}

  ```
  NAME
  kube-dal10-cr9b7371a7faaa46d08e04f046d5e6d8b4-w1
  kube-dal10-cr9b7371a7faaa46d08e04f046d5e6d8b4-w2
  ```
  {: screen}

4.  Delete the duplicate worker node in Calico. Replace NODE_ID with the worker node ID.

  ```
  calicoctl delete node NODE_ID --config=<path_to_file>/calicoctl.cfg
  ```
  {: pre}

5.  Reboot the worker node that was not deleted.

  ```
  ibmcloud oc worker reboot --cluster <cluster_name_or_id> --worker <worker_id>
  ```
  {: pre}


The deleted node is no longer listed in Calico.

<br />


## Feedback, questions, and support
{: #getting_help_workers}

Still having issues with your cluster? Review different ways to get help and support for your Red Hat OpenShift on IBM Cloud clusters. For any questions or feedback, post in Slack.
{: shortdesc}

**General ways to resolve issues**<br>
1. Keep your cluster environment up to date.
   * Check monthly for available security and operating system patches to [update your worker nodes](/docs/openshift?topic=openshift-update#worker_node).
   * [Update your cluster](/docs/openshift?topic=openshift-update#master) to the latest default version for [OpenShift](/docs/openshift?topic=openshift-openshift_versions).
2. Make sure that your command line tools are up to date.
   * In the terminal, you are notified when updates to the `ibmcloud` CLI and plug-ins are available. Be sure to keep your CLI up-to-date so that you can use all available commands and flags.
   * Make sure that [your `oc` CLI](/docs/openshift?topic=openshift-openshift-cli#cli_oc) client matches the same Kubernetes version as your cluster server. [Kubernetes does not support](https://kubernetes.io/docs/setup/release/version-skew-policy/){: external} `oc` client versions that are 2 or more versions apart from the server version (n +/- 2).
<br>

**Reviewing issues and status**<br>
1. To see whether {{site.data.keyword.cloud_notm}} is available, [check the {{site.data.keyword.cloud_notm}} status page](https://cloud.ibm.com/status?selected=status){: external}.
2. Filter for the **Kubernetes Service** component.
<br>

**Feedback and questions**<br>
1. Post in the {{site.data.keyword.containershort}} Slack.
   * If you are an external user, post in the [#openshift](https://ibm-cloud-success.slack.com/messages/CKCJLJCH4){: external} channel.
   * If you are an IBMer, use the [#iks-openshift-users](https://ibm-argonauts.slack.com/messages/CJH0UPN2D){: external} channel.<p class="tip">If you do not use an IBMid for your {{site.data.keyword.cloud_notm}} account, [request an invitation](https://cloud.ibm.com/kubernetes/slack){: external} to this Slack.</p>
2. Review forums such as OpenShift help or Stack Overflow to see whether other users ran into the same issue. When you use the forums to ask a question, tag your question so that it is seen by the {{site.data.keyword.cloud_notm}} development teams.
   * If you have technical questions about developing or deploying clusters or apps with Red Hat OpenShift on IBM Cloud, post your question on [Stack Overflow](https://stackoverflow.com/questions/tagged/ibm-cloud+containers){: external} and tag your question with `ibm-cloud`, `openshift`,  and `containers`.
   * See [Getting help](/docs/get-support?topic=get-support-getting-customer-support#using-avatar) for more details about using the forums.
<br>

**Getting help**<br>
1. Before you open a support case, gather relevant information about your cluster environment.
   1. Get your cluster details.
      ```
      ibmcloud oc cluster get -c <cluster_name_or_ID>
      ```
      {: pre}
   2. If your issue involves worker nodes, get the worker node details.
      1. List all worker nodes in the cluster, and note the **ID** of any worker nodes with an unhealthy **State** or **Status**.
         ```
         ibmcloud oc worker ls -c <cluster_name_or_ID>
         ```
         {: pre}
      2. Get the details of the unhealthy worker node.
         ```
         ibmcloud oc worker get -w <worker_ID> -c <cluster_name_or_ID>
         ```
         {: pre}
   3. For issues with resources within your cluster such as pods or services, log in to the cluster and use the Kubernetes API to get more information about them.

   You can also use the [{{site.data.keyword.containerlong_notm}} Diagnostics and Debug Tool](/docs/openshift?topic=openshift-cs_troubleshoot#debug_utility) to gather and export pertinent information to share with IBM Support.
   {: tip}

2.  Contact IBM Support by opening a case. To learn about opening an IBM support case, or about support levels and case severities, see [Contacting support](/docs/get-support?topic=get-support-getting-customer-support).
3.  In your support case, for **Category**, select **Containers**.
4.  For the **Offering**, select your OpenShift cluster. Include the relevant information that you previously gathered.


