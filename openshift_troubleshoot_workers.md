---

copyright:
  years: 2014, 2021
lastupdated: "2021-02-10"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift

---

{:DomainName: data-hd-keyref="APPDomain"}
{:DomainName: data-hd-keyref="DomainName"}
{:android: data-hd-operatingsystem="android"}
{:api: .ph data-hd-interface='api'}
{:apikey: data-credential-placeholder='apikey'}
{:app_key: data-hd-keyref="app_key"}
{:app_name: data-hd-keyref="app_name"}
{:app_secret: data-hd-keyref="app_secret"}
{:app_url: data-hd-keyref="app_url"}
{:authenticated-content: .authenticated-content}
{:beta: .beta}
{:c#: data-hd-programlang="c#"}
{:cli: .ph data-hd-interface='cli'}
{:codeblock: .codeblock}
{:curl: .ph data-hd-programlang='curl'}
{:deprecated: .deprecated}
{:dotnet-standard: .ph data-hd-programlang='dotnet-standard'}
{:download: .download}
{:external: target="_blank" .external}
{:faq: data-hd-content-type='faq'}
{:fuzzybunny: .ph data-hd-programlang='fuzzybunny'}
{:generic: data-hd-operatingsystem="generic"}
{:generic: data-hd-programlang="generic"}
{:gif: data-image-type='gif'}
{:go: .ph data-hd-programlang='go'}
{:help: data-hd-content-type='help'}
{:hide-dashboard: .hide-dashboard}
{:hide-in-docs: .hide-in-docs}
{:important: .important}
{:ios: data-hd-operatingsystem="ios"}
{:java: .ph data-hd-programlang='java'}
{:java: data-hd-programlang="java"}
{:javascript: .ph data-hd-programlang='javascript'}
{:javascript: data-hd-programlang="javascript"}
{:new_window: target="_blank"}
{:note .note}
{:note: .note}
{:objectc data-hd-programlang="objectc"}
{:org_name: data-hd-keyref="org_name"}
{:php: data-hd-programlang="php"}
{:pre: .pre}
{:preview: .preview}
{:python: .ph data-hd-programlang='python'}
{:python: data-hd-programlang="python"}
{:route: data-hd-keyref="route"}
{:row-headers: .row-headers}
{:ruby: .ph data-hd-programlang='ruby'}
{:ruby: data-hd-programlang="ruby"}
{:runtime: architecture="runtime"}
{:runtimeIcon: .runtimeIcon}
{:runtimeIconList: .runtimeIconList}
{:runtimeLink: .runtimeLink}
{:runtimeTitle: .runtimeTitle}
{:screen: .screen}
{:script: data-hd-video='script'}
{:service: architecture="service"}
{:service_instance_name: data-hd-keyref="service_instance_name"}
{:service_name: data-hd-keyref="service_name"}
{:shortdesc: .shortdesc}
{:space_name: data-hd-keyref="space_name"}
{:step: data-tutorial-type='step'}
{:subsection: outputclass="subsection"}
{:support: data-reuse='support'}
{:swift: .ph data-hd-programlang='swift'}
{:swift: data-hd-programlang="swift"}
{:table: .aria-labeledby="caption"}
{:term: .term}
{:tip: .tip}
{:tooling-url: data-tooling-url-placeholder='tooling-url'}
{:troubleshoot: data-hd-content-type='troubleshoot'}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:tsSymptoms: .tsSymptoms}
{:tutorial: data-hd-content-type='tutorial'}
{:ui: .ph data-hd-interface='ui'}
{:unity: .ph data-hd-programlang='unity'}
{:url: data-credential-placeholder='url'}
{:user_ID: data-hd-keyref="user_ID"}
{:vbnet: .ph data-hd-programlang='vb.net'}
{:video: .video}



# Worker nodes
{: #cs_troubleshoot_clusters}

As you use {{site.data.keyword.openshiftlong_notm}}, consider these techniques for general troubleshooting and debugging your cluster and cluster master.
{: shortdesc}

**General ways to resolve issues**

1. Keep your cluster environment up to date.
   * Check monthly for available security and operating system patches to [update your worker nodes](/docs/openshift?topic=openshift-update#worker_node).
   * [Update your cluster](/docs/openshift?topic=openshift-update#master) to the latest default version for [{{site.data.keyword.openshiftshort}}](/docs/containers?topic=containers-cs_versions).
2. Make sure that your command line tools are up to date.
   * In the command line, you are notified when updates to the `ibmcloud` CLI and plug-ins are available. Be sure to keep your CLI up-to-date so that you can use all available commands and flags.
   * Make sure that [your `oc` CLI](/docs/openshift?topic=openshift-openshift-cli#cli_oc) client matches the same Kubernetes version as your cluster server. [Kubernetes does not support](https://kubernetes.io/docs/setup/release/version-skew-policy/){: external} `oc` client versions that are 2 or more versions apart from the server version (n +/- 2).
<br>

**Reviewing issues and status**

1. To see whether {{site.data.keyword.cloud_notm}} is available, [check the {{site.data.keyword.cloud_notm}} status page](https://cloud.ibm.com/status?selected=status){: external}.
2. Filter for the **Kubernetes Service** component.

## Debugging worker nodes
{: #debug_worker_nodes}
{: troubleshoot}
{: support}

Review the options to debug your worker nodes and find the root causes for failures.
{: shortdesc}

**Infrastructure provider**:
  * <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
  * <img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC Generation 2 compute

1. If your cluster is in a **Critical**, **Delete failed**, or **Warning** state, or is stuck in the **Pending** state for a long time, review the state of your worker nodes.
    ```
    ibmcloud oc worker ls --cluster <cluster_name_or_id>
    ```
    {: pre}
2. Review the **State** and **Status** field for every worker node in your CLI output.
    You can view the current worker node state by running the `ibmcloud oc worker ls --cluster <cluster_name_or_ID>` command and locating the **State** and **Status** fields.
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
       <td>`Deleting`</td>
       <td>You requested to delete the worker node, possibly as part of resizing a worker pool or autoscaling the cluster. Other operations cannot be issued against the worker node while the worker node deletes. You cannot reverse the deletion process. When the deletion process completes, you are no longer billed for the worker nodes.</td>
       </tr>
       <tr>
       <td>`Deleted`</td>
       <td>Your worker node is deleted, and no longer is listed in the cluster or billed. This state cannot be undone. Any data that was stored only on the worker node, such as container images, are also deleted.</td>
       </tr>
       <tr>
       <td>`Deployed`</td>
       <td>Updates are successfully deployed to your worker node. After updates are deployed, {{site.data.keyword.openshiftlong_notm}} starts a health check on the worker node. After the health check is successful, the worker node goes into a <code>Normal</code> state. Worker nodes in a <code>Deployed</code> state usually are ready to receive workloads, which you can check by running <code>oc get nodes</code> and confirming that the state shows <code>Normal</code>. </td>
       </tr>
        <tr>
          <td>`Deploying`</td>
          <td>When you update the Kubernetes version of your worker node, your worker node is redeployed to install the updates. If you reload or reboot your worker node, the worker node is redeployed to automatically install the latest patch version. If your worker node is stuck in this state for a long time, check whether a problem occurred during the deployment. </td>
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
          <td>`Provisioned`</td>
          <td>Your worker node completed provisioning and is part of the cluster. Billing for the worker node begins. The worker node state soon reports a regular health state and status, such as `normal` and `ready`.</td>
        </tr>
     <tr>
     <tr>
          <td>`Provisioning`</td>
          <td>Your worker node is being provisioned and is not available in the cluster yet. You can monitor the provisioning process in the <strong>Status</strong> column of your CLI output. If your worker node is stuck in this state for a long time, check whether a problem occurred during the provisioning.</td>
        </tr>
     <tr>
          <td>`Provision pending`</td>
          <td>Another process is completing before the worker node provisioning process starts. You can monitor the other process that must complete first in the <strong>Status</strong> column of your CLI output. For example, in VPC clusters, the `Pending security group creation` indicates that the security group for your worker nodes is creating first before the worker nodes can be provisioned. If your worker node is stuck in this state for a long time, check whether a problem occurred during the other process.</td>
     </tr>
        <tr>
          <td>`Provision_failed`</td>
          <td>Your worker node could not be provisioned. List the details for the worker node to find the details for the failure by running `ibmcloud oc worker get --cluster <cluster_name_or_id> --worker <worker_node_id>`.</td>
        </tr>
     <tr>
          <td>`Reloading`</td>
          <td>Your worker node is being reloaded and is not available in the cluster. You can monitor the reloading process in the <strong>Status</strong> column of your CLI output. If your worker node is stuck in this state for a long time, check whether a problem occurred during the reloading.</td>
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
         <td>The Kubernetes master is not reachable for one of the following reasons:<ul><li>You requested an update of your Kubernetes master. The state of the worker node cannot be retrieved during the update. If the worker node remains in this state for an extended period of time even after the Kubernetes master is successfully updated, try to [reload](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reload) the worker node.</li><li>You might have another firewall that is protecting your worker nodes, or changed firewall settings recently. {{site.data.keyword.openshiftlong_notm}} requires certain IP addresses and ports to be opened to allow communication from the worker node to the Kubernetes master and vice versa. For more information, see [Firewall prevents worker nodes from connecting](/docs/openshift?topic=openshift-firewall#vyatta_firewall).</li><li>The Kubernetes master is down. Contact {{site.data.keyword.cloud_notm}} support by opening an [{{site.data.keyword.cloud_notm}} support case](/docs/openshift?topic=openshift-get-help).</li></ul></td>
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

**Infrastructure provider**:
  * <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
  * <img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC Generation 2 compute

  <table summary="The columns are read from left to right. The first column has the error message. The second column describes the error and provides resolution steps.">
  <caption>Common error messages</caption>
    <col width="25%">
    <thead>
    <th>Error message</th>
    <th>Description and resolution</th>
    </thead>
    <tbody>
      <tr>
        <td>Your account is currently prohibited from ordering 'Computing Instances'.</td>
        <td>Your IBM Cloud infrastructure account might be restricted from ordering compute resources. Contact {{site.data.keyword.cloud_notm}} support by opening an [{{site.data.keyword.cloud_notm}} support case](/docs/openshift?topic=openshift-get-help).</td>
      </tr>
      <tr>
      <td>Could not place order.<br><br>
      Could not place order. There are insufficient resources behind router 'router_name' to fulfill the request for the following guests: 'worker_id'.</td>
      <td>The zone that you selected might not have enough infrastructure capacity to provision your worker nodes. Or you might have exceeded a limit in your IBM Cloud infrastructure account. To resolve, try one of the following options:
      <ul><li>Infrastructure resource availability in zones can fluctuate often. Wait a few minutes and try again.</li>
      <li>For a single zone cluster, create the cluster in a different zone. For a multizone cluster, add a zone to the cluster.</li>
      <li>Specify a different pair of public and private VLANs for your worker nodes in your IBM Cloud infrastructure account. For worker nodes that are in a worker pool, you can use the <code>ibmcloud oc zone network-set</code> [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_zone_network_set).</li>
      <li>Contact your IBM Cloud infrastructure account manager to verify that you do not exceed an account limit, such as a global quota.</li>
      <li>Open an [IBM Cloud infrastructure support case](/docs/openshift?topic=openshift-get-help)</li></ul></td>
      </tr>
      <tr>
        <td>Could not obtain network VLAN with ID: <code>&lt;vlan id&gt;</code>.</td>
        <td>Your worker node could not be provisioned because the selected VLAN ID could not be found for one of the following reasons:<ul><li>You might have specified the VLAN number instead of the VLAN ID. The VLAN number is 3 or 4 digits long, whereas the VLAN ID is 7 digits long. Run <code>ibmcloud oc vlan ls --zone &lt;zone&gt;</code> to retrieve the VLAN ID.<li>The VLAN ID might not be associated with the IBM Cloud infrastructure account that you use. Run <code>ibmcloud oc vlan ls --zone &lt;zone&gt;</code> to list available VLAN IDs for your account. To change the IBM Cloud infrastructure account, see [`ibmcloud oc credential set`](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_credentials_set). </ul></td>
      </tr>
      <tr>
        <td>The location provided for this order is invalid.</td>
        <td>Your IBM Cloud infrastructure is not set up to order compute resources in the selected data center. Contact [{{site.data.keyword.cloud_notm}} support](/docs/openshift?topic=openshift-get-help) to verify that you account is set up correctly.</td>
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
  <ol><li>If you have access to multiple accounts, make sure that you are logged in to the account where you want to work with {{site.data.keyword.openshiftlong_notm}}. </li>
  <li>Run <code>ibmcloud oc api-key info --cluster &lt;cluster_name_or_ID&gt;</code> to view the current API key owner that is used to access the IBM Cloud infrastructure portfolio. </li>
  <li>Run <code>ibmcloud account list</code> to view the owner of the {{site.data.keyword.cloud_notm}} account that you currently use. </li>
  <li>Contact the owner of the {{site.data.keyword.cloud_notm}} account and report that the API key owner has insufficient permissions in IBM Cloud infrastructure or might be pending to be deleted. </li></ol>
  </br><strong>As the account owner</strong>, follow these steps:
  <ol><li>Review the [required classic permissions in IBM Cloud infrastructure](/docs/openshift?topic=openshift-users#infra_access) to perform the action that previously failed. For the VPC infrastructure provider, the API key owner must have the **Administrator** platform role.</li>
  <li>Fix the permissions of the API key owner or create a new API key by using the [<code>ibmcloud oc api-key reset --region &lt;region&gt;</code>](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_api_key_reset) command. </li>
  <li>If you or another account admin manually set IBM Cloud infrastructure credentials in your account, run [<code>ibmcloud oc credential unset --region &lt;region&gt;</code>](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_credentials_unset) to remove the credentials from your account.</li></ol></td>
  </tr>
    </tbody>
  </table>

<br />

## Unable to create or delete worker nodes or clusters
{: #infra_errors}
{: troubleshoot}
{: support}

You cannot perform infrastructure-related commands on your cluster, such as:
* Adding worker nodes in an existing cluster or when creating a new cluster
* Removing worker nodes
* Reloading or rebooting worker nodes
* Resizing worker pools
* Updating your cluster
* Deleting your cluster

Review the error messages in the following sections to troubleshoot infrastructure-related issues that are caused by [incorrect cluster permissions](#cs_credentials), [orphaned clusters in other infrastructure accounts](#orphaned), or [a time-based one-time passcode (TOTP) on the account](#cs_totp).

### Unable to create or delete worker nodes due to permission errors
{: #cs_credentials}

{: tsSymptoms}
You cannot manage worker nodes for your cluster, and you receive an error message similar to one of the following.

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
The infrastructure credentials that are set for the region and resource group are missing the appropriate [infrastructure permissions](/docs/openshift?topic=openshift-access_reference#infra). The user's infrastructure permissions are most commonly stored as an [API key](/docs/openshift?topic=openshift-users#api_key) for the region and resource group. More rarely, if you use a [different {{site.data.keyword.cloud_notm}} account type](/docs/openshift?topic=openshift-users#understand_infra), you might have [set infrastructure credentials manually](/docs/openshift?topic=openshift-users#credentials).

{: tsResolve}
The account owner must set up the infrastructure account credentials properly. The credentials depend on what type of infrastructure account you are using.

Before you begin, [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure).

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
    4.  If you manually set credentials and still cannot see the cluster's worker nodes in your infrastructure account, you might check whether the [cluster is orphaned](#orphaned).

### Unable to create or delete worker nodes due to incorrect account error
{: #orphaned}

**Infrastructure provider**: <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic

{: tsSymptoms}
You cannot manage worker nodes for your cluster, or view the cluster worker nodes in your classic IBM Cloud infrastructure account. However, you can update and manage other clusters in the account.

Further, you verified that you have the [proper infrastructure credentials](#cs_credentials).

You might receive an error message in your worker node status similar to the following.
```
Incorrect account for worker - The 'classic' infrastructure user credentials changed and no longer match the worker node instance infrastructure account.
```
{: screen}

{: tsCauses}
The cluster might be provisioned in a classic IBM Cloud infrastructure account that is no longer linked to your {{site.data.keyword.openshiftlong_notm}} account. The cluster is orphaned. Because the resources are in a different account, you do not have the infrastructure credentials to modify the resources.

Consider the following example scenario to understand how clusters might become orphaned.
1.  You have an {{site.data.keyword.cloud_notm}} Pay-As-You-Go account.
2.  You create a cluster named `Cluster1`. The worker nodes and other infrastructure resources are provisioned into the infrastructure account that comes with your Pay-As-You-Go account.
3.  Later, you find out that your team uses a legacy or shared classic IBM Cloud infrastructure account. You use the `ibmcloud oc credential set` command to change the IBM Cloud infrastructure credentials to use your team account.
4.  You create another cluster named `Cluster2`. The worker nodes and other infrastructure resources are provisioned into the team infrastructure account.
5.  You notice that `Cluster1` needs a worker node update, a worker node reload, or you just want to clean it up by deleting it. However, because `Cluster1` was provisioned into a different infrastructure account, you cannot modify its infrastructure resources. `Cluster1` is orphaned.
6.  You follow the resolution steps in the following section, but do not set your infrastructure credentials back to your team account. You can delete `Cluster1`, but now `Cluster2` is orphaned.
7.  You change your infrastructure credentials back to the team account that created `Cluster2`. Now, you no longer have an orphaned cluster!

<br>

{: tsResolve}
1.  Check which infrastructure account the region that your cluster is in currently uses to provision clusters. Replace `<region>` with the {{site.data.keyword.cloud_notm}} region that the cluster is in.
    ```sh
    ibmcloud oc credential get --region <region>
    ```
    {: pre}

    If you see a message similar to the following, then the account uses the default, linked infrastructure account.
    ```
    No credentials set for resource group <resource group>.: The user credentials could not be found.
    ```
    {: screen}
2.  Check which infrastructure account was used to provision the cluster.
    1.  In the **Worker Nodes** tab, select a worker node and note its **ID**.
    2.  Open the menu ![Menu icon](../icons/icon_hamburger.svg "Menu icon") and click **Classic Infrastructure**.
    3.  From the infrastructure navigation pane, click **Devices > Device List**.
    4.  Search for the worker node ID that you previously noted.
    5.  If you do not find the worker node ID, the worker node is not provisioned into this infrastructure account. Switch to a different infrastructure account and try again.
3.  Compare the infrastructure accounts.
    *   **If the worker nodes are in the linked infrastructure account**: Use the `ibmcloud oc credential unset` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_credentials_unset) to resume using the default infrastructure credentials that are linked with your Pay-As-You-Go account.
    *   **If the worker nodes are in a different infrastructure account**: Use the `ibmcloud oc credential set` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_credentials_set) to change your infrastructure credentials to the account that the cluster worker nodes are provisioned in, which you found in the previous step.

        If you no longer have access to the infrastructure credentials, you can open an {{site.data.keyword.cloud_notm}} support case to determine an email address for the administrator of the other infrastructure account. However, {{site.data.keyword.cloud_notm}} Support cannot remove the orphaned cluster for you, and you must contact the administrator of the other account to get the infrastructure credentials.
        {: note}
    *   **If the infrastructure accounts match**: Check the rest of the worker nodes in the cluster and see if any has a different infrastructure account. Make sure that you checked the worker nodes in the cluster that has the credentials issue. Review other [common infrastructure credential issues](#infra_errors).
4.  Now that the infrastructure credentials are updated, retry the blocked action, such as updating or deleting a worker node, and verify that the action succeeds.
5.  If you have other clusters in the same region and resource that require the previous infrastructure credentials, repeat Step 3 to reset the infrastructure credentials to the previous account. Note that if you created clusters with a different infrastructure account than the account that you switch to, you might orphan those clusters.

    Tired of switching infrastructure accounts each time you need to perform a cluster or worker action? Consider re-creating all the clusters in the region and resource group in the same infrastructure account. Then, migrate your workloads and remove the old clusters from the different infrastructure account.
    {: note}

### Unable to create or delete worker nodes due to endpoints error
{: #vpe-ts}

**Infrastructure provider**: <img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC Generation 2 compute, {{site.data.keyword.openshiftshort}} version 4.6 or later

{: tsSymptoms}
You cannot manage worker nodes for your cluster, and you receive an error message similar to one of the following.
```
Worker deploy failed due to network communications failing to master or registry endpoints. Please verify your network setup is allowing traffic from this subnet then attempt a worker replace on this worker
```
{: screen}
```
Pending endpoint gateway creation
```
{: screen}

{: tsCauses}
In clusters that run {{site.data.keyword.openshiftshort}} version 4.6 or later, worker nodes can communicate with the Kubernetes master through the cluster's virtual private endpoint (VPE). One VPE gateway resource is created per cluster in your VPC. If the VPE gateway for your cluster is not correctly created in your VPC, the VPE gateway is deleted from your VPC, or the IP address that is reserved for the VPE is deleted from your VPC subnet, worker nodes lose connectivity with the Kubernetes master.

{: tsResolve}
Re-establish the VPE connection between your worker nodes and Kubernetes master.

1. Refresh the cluster master. If the VPE gateway did not exist in your VPC, it is created, and connectivity to the reserved IP addresses on the subnets that your worker nodes are connected to is re-established. After you refresh the cluster, wait a few minutes to allow the operation to complete.
    ```
    ibmcloud oc cluster master refresh -c <cluster_name_or_ID>
    ```
    {: pre}

2. If you still cannot manage worker nodes after the cluster master is refreshed, replace the worker nodes that you cannot access.
    1. List all worker nodes in your cluster and note the **name** of the worker node that you want to replace.
       ```sh
       oc get nodes
       ```
       {: pre}

       The **name** that is returned in this command is the private IP address that is assigned to your worker node. You can find more information about your worker node when you run the `ibmcloud oc worker ls --cluster <cluster_name_or_ID>` command and look for the worker node with the same **Private IP** address.

    2. Replace the worker node. As part of the replace process, the pods that run on the worker node are drained and rescheduled onto remaining worker nodes in the cluster. The worker node is also cordoned, or marked as unavailable for future pod scheduling. Use the worker node ID that is returned from the `ibmcloud oc worker ls --cluster <cluster_name_or_ID>` command.
       ```sh
       ibmcloud oc worker replace --cluster <cluster_name_or_ID> --worker <worker_node_ID>
       ```
       {: pre}
    3. Verify that the worker node is replaced.
       ```sh
       ibmcloud oc worker ls --cluster <cluster_name_or_ID>
       ```
       {: pre}

### Unable to create or delete worker nodes due to paid account or one time password error
{: #cs_totp}

**Infrastructure provider**: <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic

{: tsSymptoms}
You cannot manage worker nodes for your cluster, and you receive an error message similar to one of the following.
```
Unable to connect to the IBM Cloud account. Ensure that you have a paid account.
```
{: screen}
```
Cannot authenticate the infrastructure user: Time-based One Time Password authentication is required to log in with this user.
```
{: screen}

{: tsCauses}
Your {{site.data.keyword.cloud_notm}} account uses its own automatically linked infrastructure through a Pay-as-you-Go account. However, the account administrator enabled the time-based one-time passcode (TOTP) option so that users are prompted for a time-based one-time passcode (TOTP) at login. This type of [multifactor authentication (MFA)](/docs/account?topic=account-types#account-based) is account-based, and affects all access to the account. TOTP MFA also affects the access that {{site.data.keyword.containerlong_notm}} requires to make calls to {{site.data.keyword.cloud_notm}} infrastructure. If TOTP is enabled for the account, you cannot create and manage clusters and worker nodes in {{site.data.keyword.containerlong_notm}}.

{: tsResolve}
The {{site.data.keyword.cloud_notm}} account owner or an account administrator must either:
* Disable TOTP for the account, and continue to use the automatically linked infrastructure credentials for {{site.data.keyword.containerlong_notm}}.
* Continue to use TOTP, but create an infrastructure API key that {{site.data.keyword.containerlong_notm}} can use to make direct calls to the {{site.data.keyword.cloud_notm}} infrastructure API.

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
    {: pre}
    Example output:
    ```
    Infrastructure credentials for user name user@email.com set for resource group default.
    ```
    {: screen}
5. To ensure that existing clusters use the updated infrastructure API credentials, run `ibmcloud oc api-key reset --region <region>` in each region where you have clusters.

<br />

## Cannot add worker nodes due to an invalid VLAN ID
{: #suspended}

**Infrastructure provider**: <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic

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

Before you begin: [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/containers?topic=containers-cs_cli_install#cs_cli_configure)

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

## Replacing a worker node does not create a worker node
{: #auto-rebalance-off}

**Infrastructure provider**:
  * <img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC Generation 2 compute

{: tsSymptoms}
When you [replace a worker node](/docs/openshift?topic=openshift-kubernetes-service-cli#cli_worker_replace) or [update a VPC worker node](/docs/openshift?topic=openshift-update#vpc_worker_node), a worker node is not automatically added back to your cluster.

{: tsCauses}
By default, your worker pools are set to automatically rebalance when you replace a worker node. However, you might have disabled automatic rebalancing by manually removing a worker node, such as in the following scenario.

1.  You have a worker pool that automatically rebalances by default.
2.  You have a troublesome worker node in the worker pool that you removed individually, such as with the `ibmcloud oc worker rm` command.
3.  Now, automatic rebalancing is disabled for your worker pool, and is not reset unless you try to rebalance or resize the worker pool.
4.  You try to replace a worker node with the `ibmcloud oc worker replace` command or update a VPC worker node with the `ibmcloud oc worker replace --update` command. The worker node is removed, but another worker node is not added back to your worker pool.

You might also have issued the `remove` command shortly after the `replace` command. If the `remove` command is processed before the `replace` command, the worker pool automatic rebalancing is still disabled, so your worker node is not replaced.
{: note}

{: tsResolve}
To enable automatical rebalancing, [rebalance](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_rebalance) or [resize](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_pool_resize) your worker pool. Now, when you replace a worker node, another worker node is created for you.

<br />

## Accessing your worker node with SSH fails
{: #cs_ssh_worker}

**Infrastructure provider**:
  * <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
  * <img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC Generation 2 compute

{: tsSymptoms}
You cannot access your worker node by using an SSH connection.

{: tsCauses}
SSH by password is unavailable on the worker nodes.

{: tsResolve}
Use a Kubernetes [`DaemonSet`](https://kubernetes.io/docs/concepts/workloads/controllers/daemonset/){: external} for actions that you must run on every node, or use jobs for one-time actions that you must run.

<br />

## Bare metal instance ID is inconsistent with worker records
{: #bm_machine_id}

**Infrastructure provider**: <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic

{: tsSymptoms}
When you use `ibmcloud oc worker` commands with your bare metal worker node, you see a message similar to the following.

```
The worker node instance ID changed. Reload the worker node if bare metal hardware was serviced.
```
{: screen}

{: tsCauses}
The machine ID can become inconsistent with the {{site.data.keyword.openshiftlong_notm}} worker record when the machine experiences hardware issues. When IBM Cloud infrastructure resolves this issue, a component can change within the system that the service does not identify.

{: tsResolve}
For {{site.data.keyword.openshiftlong_notm}} to re-identify the machine, [reload the bare metal worker node](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reload). **Note**: Reloading also updates the machine's [patch version](/docs/containers?topic=containers-changelog).

You can also [delete the bare metal worker node](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_rm). **Note**: Bare metal instances are billed monthly.

<br />

## After a worker node updates or reloads, duplicate nodes and pods appear
{: #cs_duplicate_nodes}

**Infrastructure provider**:
  * <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
  * <img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC Generation 2 compute

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

## After deleting all worker nodes, several pods do not start on new worker nodes
{: #zero_nodes_calico_failure}

**Infrastructure provider**:
  * <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
  * <img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC Generation 2 compute

{: tsSymptoms}
You deleted all worker nodes in your cluster so that zero worker nodes exist. Then, you added one or more worker nodes. When you run the following command, several pods for Kubernetes components are stuck in the `ContainerCreating` status, and the `calico-node` pods are stuck in the `CrashLoopBackOff` status.

```
oc -n kube-system get pods
```
{: pre}

{: tsCauses}
When you delete all worker nodes in your cluster, no worker node exists for the `calico-kube-controllers` pod to run on. The Calico controller pod's data cannot be updated to remove the data of the deleted worker nodes. When the Calico controller pod begins to run again on the new worker nodes, its data is not updated for the new worker nodes, and it does not start the `calico-node` pods.

{: tsResolve}
Delete the existing `calico-node` worker node entries so that new pods can be created.

**Before you begin**: Install the [Calico CLI](/docs/openshift?topic=openshift-network_policies#cli_install).

1. Run the `ibmcloud oc cluster config` command and copy and paste the output to set the `KUBECONFIG` environment variable. Include the `--admin` and `--network` options with the `ibmcloud oc cluster config` command. The `--admin` option downloads the keys to access your infrastructure portfolio and run Calico commands on your worker nodes. The `--network` option downloads the Calico configuration file to run all Calico commands.
  ```
  ibmcloud oc cluster config --cluster <cluster_name_or_ID> --admin --network
  ```
  {: pre}

2. For the `calico-node` pods that are stuck in the `CrashLoopBackOff` status, note the `NODE` IP addresses.
  ```
  oc -n kube-system get pods -o wide
  ```
  {: pre}

  In this example output, the `calico-node` pod cannot start on worker node `10.176.48.106`.
  ```
  NAME                                           READY   STATUS              RESTARTS   AGE     IP              NODE            NOMINATED NODE   READINESS GATES
  ...
  calico-kube-controllers-656c5785dd-kc9x2       1/1     Running             0          25h     10.176.48.107   10.176.48.107   <none>           <none>
  calico-node-mkqbx                              0/1     CrashLoopBackOff    1851       25h     10.176.48.106   10.176.48.106   <none>           <none>
  coredns-7b56dd58f7-7gtzr                       0/1     ContainerCreating   0          25h     172.30.99.82    10.176.48.106   <none>           <none>
  ```
  {: screen}

3. Get the IDs of the `calico-node` worker node entries. Copy the IDs for **only** the worker node IP addresses that you retrieved in the previous step.
  ```
  calicoctl get nodes -o wide
  ```
  {: pre}

4. Use the IDs to delete the worker node entries. After you delete the worker node entries, the Calico controller reschedules the `calico-node` pods on the new worker nodes.
  ```
  calicoctl delete node <node_ID>
  ```
  {: pre}

5. Verify that the Kubernetes component pods, including the `calico-node` pods, are now running. It might take a few minutes for the `calico-node` pods to be scheduled and for new component pods to be created.
  ```
  oc -n kube-system get pods
  ```
  {: pre}

To prevent this error in the future, never delete all worker nodes in your cluster. Always run at least one worker node in your cluster, and if you use Ingress or routes to expose apps, run at least two worker nodes per zone.
{: note}

<br />

## Accessing a pod on a new worker node fails with a timeout
{: #cs_nodes_duplicate_ip}

**Infrastructure provider**: <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic

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
  kube-dal10-cr9b7371a7fcbe46d08e04f046d5e6d8b4-w1   169.xx.xxx.xxx  10.xxx.xx.xxx    b3c.4x16       normal    Ready    dal10      1.18.15
  kube-dal10-cr9b7371a7fcbe46d08e04f046d5e6d8b4-w2   169.xx.xxx.xxx  10.xxx.xx.xxx    b3c.4x16       deleted    -       dal10      1.18.15
  ```
  {: screen}

2.  Install the [Calico CLI](/docs/openshift?topic=openshift-network_policies#cli_install).
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


