---

copyright:
  years: 2014, 2021
lastupdated: "2021-05-26"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift
content-type: troubleshoot

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
{:terraform: .ph data-hd-interface='terraform'}
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
  
  
# Debugging worker nodes
{: #debug_worker_nodes}
{: troubleshoot}
{: support}

Review the options to debug your worker nodes and find the root causes for failures.
{: shortdesc}

**Infrastructure provider**:
  * <img src="../images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
  * <img src="../images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC

## Step 1: Get the worker node state
{: #worker-debug-get-state}

If your cluster is in a **Critical**, **Delete failed**, or **Warning** state, or is stuck in the **Pending** state for a long time, review the state of your worker nodes.

```
ibmcloud oc worker ls --cluster <cluster_name_or_id>
```
{: pre}

## Step 2: Review the worker node state
{: #worker-debug-rev-state}

Review the **State** and **Status** field for every worker node in your CLI output.

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
        In many cases, [reloading](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_worker_reload) your worker node can solve the problem. When you reload your worker node, the latest [patch version](/docs/containers?topic=containers-cs_versions#version_types) is applied to your worker node. The major and minor version is not changed. Before you reload your worker node, make sure to cordon and drain your worker node to ensure that the existing pods are terminated gracefully and rescheduled onto remaining worker nodes. </br></br> If reloading the worker node does not resolve the issue, go to the next step to continue troubleshooting your worker node.
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
          <td>Your worker node is fully provisioned and ready to be used in the cluster. This state is considered healthy and does not require an action from the user. **Note**: Although the worker nodes might be normal, other infrastructure resources, such as [networking](/docs/containers?topic=containers-coredns_lameduck) and [storage](/docs/containers?topic=containers-debug_storage), might still need attention.</td>
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
         <td>The Kubernetes master is not reachable for one of the following reasons:<ul><li>You requested an update of your Kubernetes master. The state of the worker node cannot be retrieved during the update. If the worker node remains in this state for an extended period of time even after the Kubernetes master is successfully updated, try to [reload](/docs/containers?topic=containers-cli-plugin-kubernetes-service-cli#cs_worker_reload) the worker node.</li><li>You might have another firewall that is protecting your worker nodes, or changed firewall settings recently. {{site.data.keyword.openshiftlong_notm}} requires certain IP addresses and ports to be opened to allow communication from the worker node to the Kubernetes master and vice versa. For more information, see [Firewall prevents worker nodes from connecting](/docs/containers?topic=containers-firewall#vyatta_firewall).</li><li>The Kubernetes master is down. Contact {{site.data.keyword.cloud_notm}} support by opening an [{{site.data.keyword.cloud_notm}} support case](/docs/containers?topic=containers-get-help).</li></ul></td>
    </tr>
       <tr>
          <td>`Warning`</td>
          <td>Your worker node is reaching the limit for memory or disk space. You can either reduce work load on your worker node or add a worker node to your cluster to help load balance the work load.</td>
    </tr>
      </tbody>
    </table>

## Step 3: Get the details for each worker node
{: #worker-debug-get-details}

Get the details for the worker node. If the details include an error message, review the list of [common error messages for worker nodes](/docs/containers?topic=containers-common_worker_nodes_issues) to learn how to resolve the problem.

```
ibmcloud oc worker get --cluster <cluster_name_or_id> --worker <worker_node_id>
```
{: pre}

## Step 4: Review the infrastructure provider for the worker node
{: #worker-debug-rev-infra}

Review the infrastructure environment to check for other reasons that might cause the worker node issues.
1.  Check with your networking team to make sure that no recent maintenance, such as firewall orsubnet updates, might impact the worker node connections.
2.  Review [{{site.data.keyword.cloud_notm}}](https://cloud.ibm.com/status/){: external} for **{{site.data.keyword.openshiftlong_notm}}** and the underlying infrastructure provider, such as **Virtual Servers** for classic, **VPC** related components, or **{{site.data.keyword.satelliteshort}}**.
3.  If you have access to the underlying infrastructure, such as classic **Virtual Servers**, review the details of the corresponding machines for the worker nodes.
