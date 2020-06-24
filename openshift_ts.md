---

copyright:
  years: 2014, 2020
lastupdated: "2020-06-24"

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



# Clusters and masters
{: #cs_troubleshoot}

As you use {{site.data.keyword.openshiftlong}}, consider these techniques for general troubleshooting and debugging your cluster and cluster master.
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

## Running tests with the Diagnostics and Debug Tool
{: #debug_utility}
{: troubleshoot}
{: support}

While you troubleshoot, you can use the {{site.data.keyword.containerlong_notm}} Diagnostics and Debug Tool to run tests and gather pertinent information from your cluster.
{: shortdesc}

**Before you begin**:
If you previously installed the debug tool by using Helm, first uninstall the `ibmcloud-iks-debug` Helm chart.
1. Find the installation name of your Helm chart.
  ```
  helm list -n <project> | grep ibmcloud-iks-debug
  ```
  {: pre}

  Example output:
  ```
  <helm_chart_name> 1 Thu Sep 13 16:41:44 2019 DEPLOYED ibmcloud-iks-debug-1.0.0 default
  ```
  {: screen}

2. Uninstall the debug tool installation by deleting the Helm chart.
  ```
  helm uninstall <helm_chart_name> -n <project>
  ```
  {: pre}

3. Verify that the debug tool pods are removed. When the uninstallation is complete, no pods are returned by the following command.
  ```
  oc get pod --all-namespaces | grep ibmcloud-iks-debug
  ```
  {: pre}

</br>**To enable and use the Diagnostics and Debug Tool add-on:**

1. In your [cluster dashboard](https://cloud.ibm.com/kubernetes/clusters?platformType=openshift){: external}, click the name of the cluster where you want to install the debug tool add-on.

2. Click the **Add-ons** tab.

3. On the Diagnostics and Debug Tool card, click **Install**.

4. In the dialog box, click **Install**. Note that it can take a few minutes for the add-on to be installed. <p class="tip">To resolve some common issues that you might encounter during the add-on deployment, see [Reviewing add-on state and statuses](/docs/containers?topic=containers-cs_troubleshoot_addons#debug_addons).</p>

5. On the Diagnostics and Debug Tool card, click **Dashboard**.

6. In the debug tool dashboard, select individual tests or a group of tests to run. Some tests check for potential warnings, errors, or issues, and some tests only gather information that you can reference while you troubleshoot. For more information about the function of each test, click the information icon next to the test's name.

7. Click **Run**.

8. Check the results of each test.
  * If any test fails, click the information icon next to the test's name in the left column for information about how to resolve the issue.
  * You can also use the results of tests to gather information, such as complete YAMLs, that can help you debug your cluster in the following sections.

## Debugging clusters
{: #debug_clusters}
{: troubleshoot}
{: support}

Review the options to debug your clusters and find the root causes for failures.

1.  List your cluster and find the `State` of the cluster.

  ```
  ibmcloud oc cluster ls
  ```
  {: pre}

2.  Review the `State` of your cluster. If your cluster is in a **Critical**, **Delete failed**, or **Warning** state, or is stuck in the **Pending** state for a long time, start [debugging the worker nodes](/docs/openshift?topic=openshift-cs_troubleshoot_clusters#debug_worker_nodes).

    You can view the current cluster state by running the `ibmcloud oc cluster ls` command and locating the **State** field.
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
       <td>The deletion of the cluster is requested by the user before the Kubernetes master is deployed. After the deletion of the cluster is completed, the cluster is removed from your dashboard. If your cluster is stuck in this state for a long time, open an [{{site.data.keyword.cloud_notm}} support case](/docs/openshift?topic=openshift-cs_troubleshoot#getting_help).</td>
       </tr>
     <tr>
         <td>`Critical`</td>
         <td>The Kubernetes master cannot be reached or all worker nodes in the cluster are down. If you enabled {{site.data.keyword.keymanagementservicelong_notm}} in your cluster, the {{site.data.keyword.keymanagementserviceshort}} container might fail to encrypt or decrypt your cluster secrets. If so, you can view an error with more information when you run `oc get secrets`.</td>
        </tr>
       <tr>
         <td>`Delete failed`</td>
         <td>The Kubernetes master or at least one worker node cannot be deleted.  </td>
       </tr>
       <tr>
         <td>`Deleted`</td>
         <td>The cluster is deleted but not yet removed from your dashboard. If your cluster is stuck in this state for a long time, open an [{{site.data.keyword.cloud_notm}} support case](/docs/openshift?topic=openshift-cs_troubleshoot#getting_help). </td>
       </tr>
       <tr>
       <td>`Deleting`</td>
       <td>The cluster is being deleted and cluster infrastructure is being dismantled. You cannot access the cluster.  </td>
       </tr>
       <tr>
         <td>`Deploy failed`</td>
         <td>The deployment of the Kubernetes master could not be completed. You cannot resolve this state. Contact IBM Cloud support by opening an [{{site.data.keyword.cloud_notm}} support case](/docs/openshift?topic=openshift-cs_troubleshoot#getting_help).</td>
       </tr>
         <tr>
           <td>`Deploying`</td>
           <td>The Kubernetes master is not fully deployed yet. You cannot access your cluster. Wait until your cluster is fully deployed to review the health of your cluster.</td>
          </tr>
          <tr>
           <td>`Normal`</td>
           <td>All worker nodes in a cluster are up and running. You can access the cluster and deploy apps to the cluster. This state is considered healthy and does not require an action from you.<p class="note">Although the worker nodes might be normal, other infrastructure resources, such as [networking](/docs/openshift?topic=openshift-cs_troubleshoot_network) and [storage](/docs/openshift?topic=openshift-cs_troubleshoot_storage), might still need attention. If you just created the cluster, some parts of the cluster that are used by other services such as Ingress secrets or registry image pull secrets, might still be in process.</p></td>
        </tr>
          <tr>
           <td>`Pending`</td>
           <td>The Kubernetes master is deployed. The worker nodes are being provisioned and are not available in the cluster yet. You can access the cluster, but you cannot deploy apps to the cluster.  </td>
         </tr>
       <tr>
         <td>`Requested`</td>
         <td>A request to create the cluster and order the infrastructure for the Kubernetes master and worker nodes is sent. When the deployment of the cluster starts, the cluster state changes to <code>Deploying</code>. If your cluster is stuck in the <code>Requested</code> state for a long time, open an [{{site.data.keyword.cloud_notm}} support case](/docs/openshift?topic=openshift-cs_troubleshoot#getting_help). </td>
       </tr>
       <tr>
         <td>`Updating`</td>
         <td>The Kubernetes API server that runs in your Kubernetes master is being updated to a new Kubernetes API version. During the update, you cannot access or change the cluster. Worker nodes, apps, and resources that the user deployed are not modified and continue to run. Wait for the update to complete to review the health of your cluster. </td>
       </tr>
       <tr>
        <td>`Unsupported`</td>
        <td>The [Kubernetes version](/docs/containers?topic=containers-cs_versions#cs_versions) that the cluster runs is no longer supported. Your cluster's health is no longer actively monitored or reported. Additionally, you cannot add or reload worker nodes. To continue receiving important security updates and support, you must update your cluster. Review the [version update preparation actions](/docs/containers?topic=containers-cs_versions#prep-up), then [update your cluster](/docs/openshift?topic=openshift-update#update) to a supported Kubernetes version.</td>
       </tr>
        <tr>
           <td>`Warning`</td>
           <td><ul><li>At least one worker node in the cluster is not available, but other worker nodes are available and can take over the workload. Try to [reload](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reload) the unavailable worker nodes.</li>
           <li>Your cluster has zero worker nodes, such as if you created a cluster without any worker nodes or manually removed all the worker nodes from the cluster. [Resize your worker pool](/docs/openshift?topic=openshift-add_workers#resize_pool) to add worker nodes to recover from a `Warning` state.</li>
           <li>A control plane operation for your cluster failed. View the cluster in the console or run `ibmcloud oc cluster get --cluster <cluster_name_or_ID>` to [check the **Master Status** for further debugging](/docs/openshift?topic=openshift-cs_troubleshoot#debug_master).</li></ul></td>
        </tr>
       </tbody>
     </table>


<p>The [OpenShift master](/docs/openshift?topic=openshift-service-arch) is the main component that keeps your cluster up and running. The master stores cluster resources and their configurations in the etcd database that serves as the single point of truth for your cluster. The OpenShift API server is the main entry point for all cluster management requests from the worker nodes to the master, or when you want to interact with your cluster resources.<br><br>If a master failure occurs, your workloads continue to run on the worker nodes, but you cannot use `oc` commands to work with your cluster resources or view the cluster health until the OpenShift API server in the master is back up. If a pod goes down during the master outage, the pod cannot be rescheduled until the worker node can reach the OpenShift API server again.<br><br>During a master outage, you can still run `ibmcloud oc` commands against the {{site.data.keyword.containerlong_notm}} API to work with your infrastructure resources, such as worker nodes or VLANs. If you change the current cluster configuration by adding or removing worker nodes to the cluster, your changes do not happen until the master is back up.</p>
<p class="important">Do not restart or reboot a worker node during a master outage. This action removes the pods from your worker node. Because the Kubernetes API server is unavailable, the pods cannot be rescheduled onto other worker nodes in the cluster.</p>


<br />


## Reviewing master health
{: #debug_master}
{: troubleshoot}
{: support}

Your Red Hat OpenShift on IBM Cloud includes an IBM-managed master with highly available replicas, automatic security patch updates applied for you, and automation in place to recover in case of an incident. You can check the health, status, and state of the cluster master by running `ibmcloud oc cluster get --cluster <cluster_name_or_ID>`.
{: shortdesc}

**Master Health**<br>
The **Master Health** reflects the state of master components and notifies you if something needs your attention. The health might be one of the following:
*   `error`: The master is not operational. IBM is automatically notified and takes action to resolve this issue. You can continue monitoring the health until the master is `normal`. You can also [open an {{site.data.keyword.cloud_notm}} support case](/docs/openshift?topic=openshift-cs_troubleshoot#getting_help).
*   `normal`: The master is operational and healthy. No action is required.
*   `unavailable`: The master might not be accessible, which means some actions such as resizing a worker pool are temporarily unavailable. IBM is automatically notified and takes action to resolve this issue. You can continue monitoring the health until the master is `normal`.
*   `unsupported`: The master runs an unsupported version of Kubernetes. You must [update your cluster](/docs/openshift?topic=openshift-update) to return the master to `normal` health.

**Master Status and State**<br>
The **Master Status** provides details of what operation from the master state is in progress. The status includes a timestamp of how long the master has been in the same state, such as `Ready (1 month ago)`. The **Master State** reflects the lifecycle of possible operations that can be performed on the master, such as deploying, updating, and deleting. Each state is described in the following table.

|Master state|Description|
|--- |--- |
|`deployed`|The master is successfully deployed. Check the status to verify that the master is `Ready` or to see if an update is available.|
|`deploying`|The master is currently deploying. Wait for the state to become `deployed` before working with your cluster, such as adding worker nodes.|
|`deploy_failed`|The master failed to deploy. IBM Support is notified and works to resolve the issue. Check the **Master Status** field for more information, or wait for the state to become `deployed`.|
|`deleting`|The master is currently deleting because you deleted the cluster. You cannot undo a deletion. After the cluster is deleted, you can no longer check the master state because the cluster is completely removed.|
|`delete_failed`|The master failed to delete. IBM Support is notified and works to resolve the issue. You cannot resolve the issue by trying to delete the cluster again. Instead, check the **Master Status** field for more information, or wait for the cluster to delete. You can also [open an {{site.data.keyword.cloud_notm}} support case](/docs/openshift?topic=openshift-cs_troubleshoot#getting_help).|
|`updating`|The master is updating its Kubernetes version. The update might be a patch update that is automatically applied, or a minor or major version that you applied by updating the cluster. During the update, your highly available master can continue processing requests, and your app workloads and worker nodes continue to run. After the master update is complete, you can [update your worker nodes](/docs/openshift?topic=openshift-update#worker_node).</br></br>If the update is unsuccessful, the master returns to a `deployed` state and continues running the previous version. IBM Support is notified and works to resolve the issue. You can check if the update failed in the **Master Status** field.|
|`update_cancelled`|The master update is canceled because the cluster was not in a healthy state at the time of the update. Your master remains in this state until your cluster is healthy and you manually update the master. To update the master, use the `ibmcloud oc cluster master update` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_update).If you do not want to update the master to the default `major.minor` version during the update, include the `--version` flag and specify the latest patch version that is available for the `major.minor` version that you want, such as `1.17.7`. To list available versions, run `ibmcloud oc versions`.|
|`update_failed`|The master update failed. IBM Support is notified and works to resolve the issue. You can continue to monitor the health of the master until the master reaches a normal state. If the master remains in this state for more than 1 day, [open an {{site.data.keyword.cloud_notm}} support case](/docs/openshift?topic=openshift-cs_troubleshoot#getting_help). IBM Support might identify other issues in your cluster that you must fix before the master can be updated.|
{: caption="Master states"}
{: summary="Table rows read from left to right, with the master state in column one and a description in column two."}


<br />




## Debugging OpenShift web console, OperatorHub, internal registry, and other components
{: #oc_console_fails}

OpenShift clusters have many built-in components that work together to simplify the developer experience. For example, you can use the OpenShift web console to manage and deploy your cluster workloads, or enable 3rd-party operators from the OperatorHub to enhance your cluster with a service mesh and other capabilities.  
{: shortdesc}

Commonly used components include the following:
* **OpenShift web console** in the `openshift-console` project
* **OperatorHub** in the `openshift-marketplace` project
* **Internal registry** in the `openshift-image-registry` project

If these components fail, review the following debug steps.

<img src="images/icon-version-43.png" alt="Version 4.3 icon" width="30" style="width:30px; border-style: none"/> Some components, such as the OperatorHub, are available only in clusters that run OpenShift version 4.3 or later, or run in different projects in version 3.11. You can still troubleshoot OpenShift components in 3.11 clusters, but the project and resource names might vary.
{: note}

1.  Check that your {{site.data.keyword.cloud_notm}} account is set up properly. Some common scenarios that can prevent the default components from running properly include the following:
    * If you have a firewall, make sure that [open the required ports and IP addresses in your firewall](/docs/openshift?topic=openshift-firewall) so that you do not block any ingress or egress traffic for the OperatorHub or other OpenShift components.
    * If your cluster has multiple zones, or if you have a VPC cluster, make sure that you enable [VRF or VLAN spanning](/docs/openshift?topic=openshift-subnets#basics_segmentation). To check if VRF is already enabled, run `ibmcloud account show`. To check if VLAN spanning is enabled, run `ibmcloud oc vlan-spanning get`.
    * Make sure that your account does not use multifactor authentication (MFA). For more information, see [Disabling required MFA for all users in your account](/docs/iam?topic=iam-enablemfa#disablemfa).
2. VPC clusters: Check that a public gateway is enabled on each VPC subnet that your cluster is attached to. Public gateway are required for default components such as the web console and OperatorHub to use a secure, public connection to complete actions such as pulling images from remote, private registries.
    1. Use the {{site.data.keyword.cloud_notm}} console or CLI to [ensure that a public gateway is enabled on each subnet](#create_vpc_subnet) that your cluster is attached to.
    2. Restart the components for the **Developer catalog** in the web console.
        1. Edit the configmap for the samples operator.
          ```
          oc edit configs.samples.operator.openshift.io/cluster
          ```
          {: pre}
        2. Change the value of `managementState` from `Removed` to `Managed`.
        3. Save and close the config map. Your changes are automatically applied.

3.  Check that your cluster is set up properly. If you just created your cluster, wait awhile for your cluster components to fully provision.
    1.  Get the details of your cluster.
        ```
        ibmcloud oc cluster get -c <cluster_name_or_ID>
        ```
        {: pre}
    2.  Review the output of the previous step to check the **Ingress Subdomain**.
        *  If your cluster does **not** have a subdomain, see [No Ingress subdomain exists after cluster creation](/docs/openshift?topic=openshift-cs_troubleshoot_debug_ingress#ingress_subdomain).
        *  If your cluster does have a subdomain, continue to the next step.
    3.  Verify that your cluster runs the latest **Version**. If your cluster does not run the latest version, update the cluster and worker nodes.
        1.  [Update the cluster master](/docs/openshift?topic=openshift-update#master) to the latest version.

            **4.3**:
            ```
            ibmcloud oc cluster master update -c <cluster_name_or_ID> --version 4.3_openshift -f
            ```
            {: pre}

            **3.11**:
            ```
            ibmcloud oc cluster master update -c <cluster_name_or_ID> --version 3.11_openshift -f
            ```
            {: pre}

        2.  List your worker nodes.
            ```
            ibmcloud oc worker ls -c <cluster_name_or_ID>
            ```
            {: pre}
        3.  [Update the worker nodes](/docs/openshift?topic=openshift-update#worker_node) to match the cluster master version.
            ```
            ibmcloud oc worker update -c <cluster_name_or_ID> -w <worker1_ID> -w <worker2_ID> -w <worker3_ID>
            ```
            {: pre}
    4.  Check the cluster **State**. If the state is not **normal**, see [Debugging clusters](#debug_clusters).
    5.  Check the **Master health**. If the state is not **normal**, see [Reviewing master health](#debug_master).
    6.  Check the worker nodes that the OpenShift components might run on. If the state is not **normal**, see [Debugging worker nodes](/docs/openshift?topic=openshift-cs_troubleshoot_clusters#debug_worker_nodes).
        ```
        ibmcloud oc worker ls -c <cluster_name_or_ID>
        ```
        {: pre}
3.  [Log in to your cluster](/docs/openshift?topic=openshift-access_cluster). Note that if the OpenShift web console does not work for you to get the login token, you can [access the cluster from the CLI](/docs/openshift?topic=openshift-access_cluster#access_oc_cli).
4.  Check the health of the OpenShift component pods that do not work.
    1.  Check the status of the pod.
        ```
        oc get pods -n <project>
        ```
        {: pre}
    2.  If a pod is not in a **Running** status, describe the pod and check for the events. For example, you might see an error that the pod cannot be scheduled because of a lack of CPU or memory resources, which is common if you have a cluster with less than 3 worker nodes. [Resize your worker pool](/docs/openshift?topic=openshift-add_workers) and try again.
        ```
        oc describe pod -n <project> <pod>
        ```
        {: pre}

    3.  If you do not see any helpful information in the events section, check the pod logs for any error messages or other troubleshooting information.
        ```
        oc logs pod -n <project> <pod>
        ```
        {: pre}
    4.  Restart the pod and check if it reaches a **Running** status.
        ```
        oc delete pod -n <project> <pod>
        ```
        {: pre}
5.  If the pods are healthy, check if other system pods are experiencing issues. Oftentimes to function properly, one component depends on another component to be healthy. For example, the OperatorHub has a set of images that are stored in external registries such as `quay.io`. These images are pulled into the internal registry to use across the projects in your OpenShift cluster. If any of the OperatorHub or internal registry components are not set up properly, such as due to lack of permissions or compute resources, the OperatorHub and catalog do not display.
    1.  Check for pending pods.
        ```
        oc get pods --all-namespaces | grep Pending
        ```
        {: pre}
    2.  Describe the pods and check for the **Events**.
        ```
        oc describe pod -n <project_name> <pod_name>
        ```
        {: pre}

        For example, some common messages that you might see from `openshift-image-registry` pods include:
        * A `Volume could not be created` error message because you created the cluster without the correct storage permission. Red Hat OpenShift on IBM Cloud clusters come with a file storage device by default to store images for the system and other pods. Revise your [infrastructure permissions](/docs/openshift?topic=openshift-access_reference#infra) and restart the pod.
        * An `order will exceed maximum number of storage volumes allowed` error message because you have exceeded the combined quota of file and block storage devices that are allowed per account. [Remove unused storage devices](/docs/openshift?topic=openshift-file_storage#cleanup) or [increase your storage quota](/docs/FileStorage?topic=FileStorage-managinglimits), and restart the pod.
        * A message that images cannot be stored because the file storage device is full. [Resize the storage device](/docs/openshift?topic=openshift-file_storage#file_change_storage_configuration) and restart the pod.
        * A `Pull image still failed due to error: unauthorized: authentication required` error message because the internal registry cannot pull images from an external registry. Check that [the image pull secrets](/docs/openshift?topic=openshift-registry#cluster_registry_auth) are set for the project and restart the pod.
    3.  Check the **Node** that the failing pods run on. If all the pods run on the same worker node, the worker node might have a network connectivity issue. Reload the worker node.
        ```
        ibmcloud oc worker reload -c <cluster_name_or_ID> -w <worker_node_ID>
        ```
        {: pre}
6.  Check that the OpenVPN in the cluster is set up properly.
    1.  Check that the OpenVPN pod is **Running**.
        ```
        oc get pods -n kube-system -l app=vpn
        ```
        {: pre}
    2.  Check the OpenVPN logs, and check for an `ERROR` message such as `WORKERIP:<port>`, such as `WORKERIP:10250`, that indicates that the VPN tunnel does not work.
        ```
        oc logs -n kube-system <vpn_pod> --tail 10
        ```
        {: pre}
    3.  If you see the worker IP error, check if worker-to-worker communication is broken. Log in to a `calico-node` pod in the `calico-system` project, and check for the same `WORKERIP:10250` error.
        ```
        oc exec -n calico-system <calico-node_pod> -- date
        ```
        {: pre}
    4.  If the worker-to-worker communication is broken, make sure that you enable [VRF or VLAN spanning](/docs/openshift?topic=openshift-subnets#basics_segmentation).
    5.  If you see a different error from either the OpenVPN or `calico-node` pod, restart the OpenVPN pod.
        ```
        oc delete pod -n kube-system <vpn_pod>
        ```
        {: pre}
    6.  If the OpenVPN still fails, check the worker node that the pod runs on.
        ```
        oc describe pod -n kube-system <vpn_pod> | grep "Node:"
        ```
        {: pre}
    7.  Cordon the worker node so that the OpenVPN pod is rescheduled to a different worker node.
        ```
        oc cordon <worker_node>
        ```
        {: pre}
    8.  Check the OpenVPN pod logs again. If the pod no longer has an error, the worker node might have a network connectivity issue. Reload the worker node.
        ```
        ibmcloud oc worker reload -c <cluster_name_or_ID> -w <worker_node_ID>
        ```
        {: pre}
7.  Refresh the cluster master to set up the default OpenShift components. After you refresh the cluster, wait a few minutes to allow the operation to complete.
    ```
    ibmcloud oc cluster master refresh -c <cluster_name_or_ID>
    ```
    {: pre}
7.  Try to use the OpenShift component again. If the error still exists, see [Feedback, questions, and support](#getting_help).

<br />




## Common CLI issues
{: #ts_clis}
{: troubleshoot}
{: support}

Review the following common reasons for CLI connection issues or command failures.

### Firewall prevents running CLI commands
{: #ts_firewall_clis}

{: tsSymptoms}
When you run `ibmcloud`, `kubectl`,`oc`,  or `calicoctl` commands from the CLI, they fail.

{: tsCauses}
You might have corporate network policies that prevent access from your local system to public endpoints via proxies or firewalls.

{: tsResolve}
[Allow TCP access for the CLI commands to work](/docs/openshift?topic=openshift-firewall#firewall_bx). This task requires the [**Administrator** {{site.data.keyword.cloud_notm}} IAM platform role](/docs/openshift?topic=openshift-users#platform) for the cluster.

<br />


### `kubectl` or `oc` commands do not work
{: #kubectl_fails}

{: tsSymptoms}
When you run `kubectl` or `oc` commands against your cluster, your commands fail with an error message similar to the following.

```
No resources found.
Error from server (NotAcceptable): unknown (get nodes)
```
{: screen}

```
invalid object doesn't have additional properties
```
{: screen}

```
error: No Auth Provider found for name "oidc"
```
{: screen}

{: tsCauses}
You have a different version of `kubectl` than your cluster version. [Kubernetes does not support](https://kubernetes.io/docs/setup/release/version-skew-policy/){: external} `kubectl` client versions that are 2 or more versions apart from the server version (n +/- 2). If you use a community Kubernetes cluster, you might also have the OpenShift version of `kubectl`, which does not work with community Kubernetes clusters.

To check your client `kubectl` version against the cluster server version, run `oc version --short`.

{: tsResolve}
[Install the version of `kubectl`](/docs/openshift?topic=openshift-openshift-cli#cli_oc) that matches the Kubernetes version of your cluster.

If you have multiple clusters at different Kubernetes versions or different container platforms such as OpenShift, download each `kubectl` version binary file to a separate directory. Then, you can set up an alias in your local terminal profile to point to the `kubectl` binary file directory that matches the `kubectl` version of the cluster that you want to work with, or you might be able to use a tool such as `brew switch kubernetes-cli <major.minor>`.

<br />



### Time out when trying to connect to a pod
{: #roks_timeout}

{: tsSymptoms}
You try to connect to a pod, such as logging in with `oc exec` or getting logs with `oc logs`. The pod is healthy, but you see an error message similar to the following.
```
Error from server: Get https://<10.xxx.xx.xxx>:<port>/<address>: dial tcp <10.xxx.xx.xxx>:<port>: connect: connection timed out
```
{: screen}

{: tsCauses}
The OpenVPN server is experiencing configuration issues that prevent accessing the pod from its internal address.

{: tsResolve}
Before you begin: [Access your OpenShift cluster](/docs/openshift?topic=openshift-access_cluster).

1.  Check if a cluster and worker node updates are available by viewing your cluster and worker node details in the console or a `cluster ls` or `worker ls` command. If so, [update your cluster and worker nodes to the latest version](/docs/openshift?topic=openshift-update).
2.  Restart the OpenVPN pod by deleting it. Another VPN pod is scheduled. When its **STATUS** is **Running**, try to connect the pod that you previously could not connect to.
    ```
    oc delete pod -n kube-system -l app=vpn
    ```
    {: pre}

### Missing projects or `oc` and `kubectl` commands fail
{: #rhoks_ts_admin_config}
{: troubleshoot}
{: support}

{: tsSymptoms}
You do not see all the projects that you have access to. When you try to run `oc` or `kubectl` commands, you see an error similar to the following.
```
No resources found.
Error from server (Forbidden): <resource> is forbidden: User "IAM#user@email.com" cannot list <resources> at the cluster scope: no RBAC policy matched
```
{: screen}

{: tsCauses}
You need to download the `admin` configuration files for your cluster in order to run commands that require the `cluster-admin` cluster role.

{: tsResolve}
Run `ibmcloud oc cluster config --cluster <cluster_name_or_ID> --admin` and try again.


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





## Unable to create a cluster in the console due to `No VPC is available` error
{: #ts_no_vpc}

{: tsSymptoms}
You try to create a VPC cluster by using the [Red Hat OpenShift on IBM Cloud console](https://cloud.ibm.com/kubernetes/catalog/create){: external}. You have an existing [VPC for Generation 1 compute](https://cloud.ibm.com/vpc){: external} in your account, but when you try to select an existing **Virtual Private Cloud** to create the cluster in, you see the following error message:
```
No VPC is available. Create a VPC.
```
{: screen}

{: tsCauses}
During cluster creation, the Red Hat OpenShift on IBM Cloud console uses the API key that is set for the `default` resource group to list the VPCs that are available in your {{site.data.keyword.cloud_notm}} account. If no API key is set for the `default` resource group, no VPCs are listed in the Red Hat OpenShift on IBM Cloud console, even if your VPC exists in a different resource group and an API key is set for that resource group.

{: tsResolve}
To set an API key for the `default` resource group, use the Red Hat OpenShift on IBM Cloud CLI.
1. Log in to the terminal as the account owner. If you want a different user than the account owner to set the API key, first [ensure that the API key owner has the correct permissions](/docs/openshift?topic=openshift-users#owner_permissions).
    ```
    ibmcloud login [--sso]
    ```
    {: pre}

2. Target the `default` resource group.
    ```
    ibmcloud target -g default
    ```
    {:pre}

3. Set the API key for the region and resource group.
    ```
    ibmcloud oc api-key reset --region <region>
    ```
    {: pre}

4. In the [Red Hat OpenShift on IBM Cloud console](https://cloud.ibm.com/kubernetes/catalog/create){: external}, click **Refresh VPCs**. Your available VPCs are now listed in a drop-down menu.

<br />




## Cluster create error about cloud object storage bucket
{: #ts_cos_bucket_cluster_create}

{: tsSymptoms}
When you create a cluster, you see an error message similar to the following.

```
Could not store the cloud object storage bucket and IAM service key.
```
{: screen}

```
Could not find the specified cloud object storage instance.
```
{: screen}

```
Could not create an IAM service key to access the cloud object storage bucket '{{.Name}}'.
```
{: screen}

```
Could not create a bucket in your cloud object storage instance.
```
{: screen}

```
Your cluster is created, but the internal registry is not backed up to cloud object storage. For more information, see 'http://ibm.biz/roks_cos_ts'.
```
{: screen}

{: tsCauses}
When you create a Red Hat OpenShift on IBM Cloud version 4 cluster on VPC generation 2 compute infrastructure, a bucket is automatically created in a standard {{site.data.keyword.cos_full_notm}} instance that you select in your account. However, the bucket might not create for several reasons such as:
* {{site.data.keyword.cos_full_notm}} is temporarily unavailable.
* No standard {{site.data.keyword.cos_full_notm}} instance exists in your account.
* The person who created your cluster did not have the **Administrator** platform role to {{site.data.keyword.cos_full_notm}} in IAM.
* The service failed to set up service key access to the object storage instance, such as if the API key lacks permissions or {{site.data.keyword.cloud_notm}} IAM is unavailable.
* Other conflicts, such as naming conflicts that exhaust the preset number of retries or saving the bucket and service key data in the backend service.

Your cluster is still created, but the internal registry is not backed up to {{site.data.keyword.cos_full_notm}}. Instead, data is saved to the `emptyDir` directory on the local worker nodes, which is not persistent storage.

{: tsResolve}
Manually set up your cluster to back up the internal registry to an {{site.data.keyword.cos_full_notm}} bucket.

1. [Log in to your account. If applicable, target the appropriate resource group. Set the context for your cluster.](/docs/openshift?topic=openshift-cs_cli_install#cs_cli_configure)
2. [Create a standard {{site.data.keyword.cos_full_notm}} service, at least one bucket, and HMAC service credentials](/docs/openshift?topic=openshift-object_storage#create_cos_service).
3. [Create a Kubernetes secret](/docs/openshift?topic=openshift-object_storage#create_cos_secret) in the `openshift-image-registry` namespace that uses your COS `access_key_id` and `secret_access_key`.
    ```
    oc create secret generic image-registry-private-configuration-user --from-literal=REGISTRY_STORAGE_S3_ACCESSKEY=<access_key_id> --from-literal=REGISTRY_STORAGE_S3_SECRETKEY=<secret_access_key> --namespace openshift-image-registry
    ```
    {: pre}

4. Edit the OpenShift Registry Operator to use {{site.data.keyword.cos_full_notm}} as a backing store.
    ```
    oc edit configs.imageregistry.operator.openshift.io/cluster
    ```
    {: pre}

5. Add the following parameters to the `spec` section of the configmap, then save and close the file. To pick up the configuration change, the `openshift-image-registry` pods automatically restart.
    ```yaml
      storage:
        s3:
            bucket: <bucket_name> # Example: my-bucket
            encrypt: false
            keyID: ""
            region: <region> # Example: us-east
            regionEndpoint: s3.<region>.cloud-object-storage.appdomain.cloud
    ```
    {: codeblock}

6.  Verify that the internal registry images are backed up to {{site.data.keyword.cos_full_notm}}.
    1.  [Build an image for your app](/docs/openshift?topic=openshift-images) and [push it to {{site.data.keyword.registrylong_notm}}](/docs/openshift?topic=openshift-images#push-images).
    2.  [Import the image into your internal OpenShift registry](/docs/openshift?topic=openshift-registry#imagestream_registry).
    3.  [Deploy an app](/docs/openshift?topic=openshift-images#pod_imagePullSecret) that references your image.
    4.  From the [{{site.data.keyword.cloud_notm}} console resource list](https://cloud.ibm.com/resources), select your **Cloud Object Storage** instance.
    5.  From the menu, click **Buckets**, then click the bucket that you used for your Red Hat OpenShift on IBM Cloud cluster.
    6.  Review the recent **Objects** to see your backed up images from the internal registry of your Red Hat OpenShift on IBM Cloud cluster.

<br />




## Cluster create error cannot pull images from {{site.data.keyword.registrylong_notm}}
{: #ts_image_pull_create}

{: tsSymptoms}
When you created a cluster, you received an error message similar to the following.


```
Your cluster cannot pull images from the {{site.data.keyword.registrylong_notm}} 'icr.io' domains because an IAM access policy could not be created. Make sure that you have the IAM Administrator platform role to {{site.data.keyword.registrylong_notm}}. Then, create an image pull secret with IAM credentials to the registry by running 'ibmcloud ks cluster pull-secret apply'.
```
{: screen}

{: tsCauses}
During cluster creation, a service ID is created for your cluster and assigned the **Reader** service access policy to {{site.data.keyword.registrylong_notm}}. Then, an API key for this service ID is generated and stored in [an image pull secret](/docs/openshift?topic=openshift-registry#cluster_registry_auth) to authorize the cluster to pull images from {{site.data.keyword.registrylong_notm}}.

To successfully assign the **Reader** service access policy to the service ID during cluster creation, you must have the **Administrator** platform access policy to {{site.data.keyword.registrylong_notm}}.

{: tsResolve}

Steps:
1.  Make sure that the account owner gives you the **Administrator** role to {{site.data.keyword.registrylong_notm}}.
    ```
    ibmcloud iam user-policy-create <your_user_email> --service-name container-registry --roles Administrator
    ```
    {: pre}
2.  [Use the `ibmcloud oc cluster pull-secret apply` command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_cluster_pull_secret_apply) to re-create an image pull secret with the appropriate registry credentials.

<br />


## Cluster cannot update because of broken webhook
{: #webhooks_update}

{: tsSymptoms}
During a master operation such as updating your cluster version, the cluster had a broken webhook application. Now, master operations cannot complete. You see an error similar to the following:

```
Cannot complete cluster master operations because the cluster has a broken webhook application. For more information, see the troubleshooting docs: 'https://ibm.biz/master_webhook'
```
{: screen}

{: tsCauses}
Your cluster has configurable Kubernetes webhook resources, validating or mutating admission webhooks, that can intercept and modify requests from various services in the cluster to the API server in the cluster master. Because webhooks can change or reject requests, broken webhooks can impact the functionality of the cluster in various ways, such as preventing you from updating the master version or other maintenance operations. For more information, see the [Dynamic Admission Control](https://kubernetes.io/docs/reference/access-authn-authz/extensible-admission-controllers/){: external} in the Kubernetes documentation.

Potential causes for broken webhooks include:
*   The underlying resource that issues the request is missing or unhealthy, such as a Kubernetes service, endpoint, or pod.
*   The webhook is part of an add-on or other plug-in application that did not install correctly or is unhealthy.
*   Your cluster might have a networking connectivity issue that prevents the webhook from communicating with the Kubernetes API server in the cluster master.

{: tsResolve}
Identify and restore the resource that causes the broken webhook.

1.  Create a test pod to get an error that identifies the broken webhook. The error message might have the name the broken webhook.
    ```
    oc run webhook-test --generator=run-pod/v1 --image pause:latest
    ```
    {: pre}

    In the following example, the webhook is `trust.hooks.securityenforcement.admission.cloud.ibm.com`.
    ```
    Error from server (InternalError): Internal error occurred: failed calling webhook "trust.hooks.securityenforcementadmission.cloud.ibm.com": Post https://ibmcloud-image-enforcement.ibm-system.svc:443/mutating-pods?timeout=30s: dialtcp 172.21.xxx.xxx:443: connect: connection timed out
    ```
    {: screen}
2.  Get the name of the broken webhook.
    *   If the error message has a broken webhook, replace `trust.hooks.securityenforcement.admission.cloud.ibm.com` with the broken webhook that you previously identified.
        ```
        oc get mutatingwebhookconfigurations,validatingwebhookconfigurations -o jsonpath='{.items[?(@.webhooks[*].name=="trust.hooks.securityenforcement.admission.cloud.ibm.com")].metadata.name}{"\n"}'
        ```
        {: pre}

        Example output:
        ```
        image-admission-config
        ```
        {: pre}
    *   If the error does not have a broken webhook, list all the webhooks in your cluster and check their configurations in the following steps.
        ```
        oc get mutatingwebhookconfigurations,validatingwebhookconfigurations
        ```
        {: pre}   
3.  Review the service and location details of the mutating or validating webhook configuration in the `clientConfig` section in the output of the following command. Replace `image-admission-config` with the name that you previously identified. If the webhook exists outside the cluster, contact the cluster owner to check the webhook status.
    ```
    oc get mutatingwebhookconfiguration image-admission-config -o yaml
    ```
    {: pre}

    ```
    oc get validatingwebhookconfigurations image-admission-config -o yaml
    ```
    {: pre}

    Example output:
    ```
      clientConfig:
        caBundle: <redacted>
        service:
            name: <name>
            namespace: <namespace>
            path: /inject
            port: 443
    ```
    {: screen}
4.  **Optional**: Back up the webhooks, especially if you do not know how to reinstall the webhoook.
    ```
    oc get mutatingwebhookconfiguration <name> -o yaml > mutatingwebhook-backup.yaml
    ```
    {: pre}

    ```
    oc get validatingwebhookconfiguration <name> -o yaml > validatingwebhook-backup.yaml
    ```
    {: pre}
5.  Check the status of the related service and pods for the webhook.
    1.  Check the service **Type**, **Selector**, and **Endpoint** fields.
        ```
        oc describe service -n <namespace> <service_name>
        ```
        {: pre}
    2.  If the service type is **ClusterIP**, check that the OpenVPN pod is in a **Running** status so that the webhook can connect securely to the Kubernetes API in the cluster master. If the pod is not healthy, check the pod events, logs, worker node health, and other components to troubleshoot. For more information, see [Debugging app deployments](/docs/openshift?topic=openshift-cs_troubleshoot_app).
        ```
        oc describe pods -n kube-system -l app=vpn
        ```
        {: pre}
    3.  If the service does not have an endpoint, check the health of the backing resources, such as a deployment or pod. If the resource is not healthy, check the pod events, logs, worker node health, and other components to troubleshoot. For more information, see [Debugging app deployments](/docs/openshift?topic=openshift-cs_troubleshoot_app).
        ```
        oc get all -n my-service-namespace -l <key=value>
        ```
        {: pre}
    4.  If the service does not have any backing resources, or if troubleshooting the pods does not resolve the issue, remove the webhook.
        ```
        oc delete mutatingwebhook <name>
        ```
        {: pre}
6.  Retry the cluster master operation, such as updating the cluster.
7.  If you still see the error, you might have worker node or network connectivity issues.
    *   [Worker node troubleshooting](/docs/openshift?topic=openshift-cs_troubleshoot_clusters).
    *   Make sure that the webhook can connect to the Kubernetes API server in the cluster master. For example, if you use Calico network policies, security groups, or some other type of firewall, set up your [classic](/docs/openshift?topic=openshift-firewall) or [VPC](/docs/openshift?topic=openshift-vpc-firewall) cluster with the appropriate access.
    *   If the webhook is managed by an add-on that you installed, uninstall the add-on. Common add-ons that cause webhook issues include the following:
        * [Container image security enforcement](/docs/Registry?topic=Registry-security_enforce).
8.  Re-create the webhook or reinstall the add-on.

<br />


## Cluster remains in a pending State
{: #cs_cluster_pending}

{: tsSymptoms}
When you deploy your cluster, it remains in a pending state and doesn't start.

{: tsCauses}
If you just created the cluster, the worker nodes might still be configuring. If you already wait for a while, you might have an invalid VLAN.

{: tsResolve}

You can try one of the following solutions:
  - Check the status of your cluster by running `ibmcloud oc cluster ls`. Then, check to be sure that your worker nodes are deployed by running `ibmcloud oc worker ls --cluster <cluster_name>`.
  - Check to see whether your VLAN is valid. To be valid, a VLAN must be associated with infrastructure that can host a worker with local disk storage. You can [list your VLANs](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_vlans) by running `ibmcloud oc vlan ls --zone <zone>` if the VLAN does not show in the list, then it is not valid. Choose a different VLAN.

<br />



## Unable to view or work with a cluster
{: #cs_cluster_access}

{: tsSymptoms}
* You are not able to find a cluster. When you run `ibmcloud oc cluster ls`, the cluster is not listed in the output.
* You are not able to work with a cluster. When you run `ibmcloud oc cluster config` or other cluster-specific commands, the cluster is not found.


{: tsCauses}
In {{site.data.keyword.cloud_notm}}, each resource must be in a resource group. For example, cluster `mycluster` might exist in the `default` resource group. When the account owner gives you access to resources by assigning you an {{site.data.keyword.cloud_notm}} IAM platform role, the access can be to a specific resource or to the resource group. When you are given access to a specific resource, you don't have access to the resource group. In this case, you don't need to target a resource group to work with the clusters you have access to. If you target a different resource group than the group that the cluster is in, actions against that cluster can fail. Conversely, when you are given access to a resource as part of your access to a resource group, you must target a resource group to work with a cluster in that group. If you don't target your CLI session to the resource group that the cluster is in, actions against that cluster can fail.

If you cannot find or work with a cluster, you might be experiencing one of the following issues:
* You have access to the cluster and the resource group that the cluster is in, but your CLI session is not targeted to the resource group that the cluster is in.
* You have access to the cluster, but not as part of the resource group that the cluster is in. Your CLI session is targeted to this or another resource group.
* You don't have access to the cluster.

{: tsResolve}
To check your user access permissions:

1. List all of your user permissions.
    ```
    ibmcloud iam user-policies <your_user_name>
    ```
    {: pre}

2. Check if you have access to the cluster and to the resource group that the cluster is in.
    1. Look for a policy that has a **Resource Group Name** value of the cluster's resource group and a **Memo** value of `Policy applies to the resource group`. If you have this policy, you have access to the resource group. For example, this policy indicates that a user has access to the `test-rg` resource group:
        ```
        Policy ID:   3ec2c069-fc64-4916-af9e-e6f318e2a16c
        Roles:       Viewer
        Resources:
                     Resource Group ID     50c9b81c983e438b8e42b2e8eca04065
                     Resource Group Name   test-rg
                     Memo                  Policy applies to the resource group
        ```
        {: screen}
    2. Look for a policy that has a **Resource Group Name** value of the cluster's resource group, a **Service Name** value of `containers-kubernetes` or no value, and a **Memo** value of `Policy applies to the resource(s) within the resource group`. If you this policy, you have access to clusters or to all resources within the resource group. For example, this policy indicates that a user has access to clusters in the `test-rg` resource group:
        ```
        Policy ID:   e0ad889d-56ba-416c-89ae-a03f3cd8eeea
        Roles:       Administrator
        Resources:
                     Resource Group ID     a8a12accd63b437bbd6d58fb6a462ca7
                     Resource Group Name   test-rg
                     Service Name          containers-kubernetes
                     Service Instance
                     Region
                     Resource Type
                     Resource
                     Memo                  Policy applies to the resource(s) within the resource group
        ```
        {: screen}
    3. If you have both of these policies, skip to Step 4, first bullet. If you don't have the policy from Step 2a, but you do have the policy from Step 2b, skip to Step 4, second bullet. If you do not have either of these policies, continue to Step 3.

3. Check if you have access to the cluster, but not as part of access to the resource group that the cluster is in.
    1. Look for a policy that has no values besides the **Policy ID** and **Roles** fields. If you have this policy, you have access to the cluster as part of access to the entire account. For example, this policy indicates that a user has access to all resources in the account:
        ```
        Policy ID:   8898bdfd-d520-49a7-85f8-c0d382c4934e
        Roles:       Administrator, Manager
        Resources:
                     Service Name
                     Service Instance
                     Region
                     Resource Type
                     Resource
        ```
        {: screen}
    2. Look for a policy that has a **Service Name** value of `containers-kubernetes` and a **Service Instance** value of the cluster's ID. You can find a cluster ID by running `ibmcloud oc cluster get --cluster <cluster_name>`. For example, this policy indicates that a user has access to a specific cluster:
        ```
        Policy ID:   140555ce-93ac-4fb2-b15d-6ad726795d90
        Roles:       Administrator
        Resources:
                     Service Name       containers-kubernetes
                     Service Instance   df253b6025d64944ab99ed63bb4567b6
                     Region
                     Resource Type
                     Resource
        ```
        {: screen}
    3. If you have either of these policies, skip to the second bullet point of step 4. If you do not have either of these policies, skip to the third bullet point of step 4.

4. Depending on your access policies, choose one of the following options.
    * If you have access to the cluster and to the resource group that the cluster is in:
      1. Target the resource group. **Note**: You can't work with clusters in other resource groups until you untarget this resource group.
          ```
          ibmcloud target -g <resource_group>
          ```
          {: pre}

      2. Target the cluster.
          ```
          ibmcloud oc cluster config --cluster <cluster_name_or_ID>
          ```
          {: pre}

    * If you have access to the cluster but not to the resource group that the cluster is in:
      1. Do not target a resource group. If you already targeted a resource group, untarget it:
        ```
        ibmcloud target --unset-resource-group
        ```
        {: pre}

      2. Target the cluster.
        ```
        ibmcloud oc cluster config --cluster <cluster_name_or_ID>
        ```
        {: pre}

    * If you do not have access to the cluster:
        1. Ask your account owner to assign an [{{site.data.keyword.cloud_notm}} IAM platform role](/docs/openshift?topic=openshift-users#platform) to you for that cluster.
        2. Do not target a resource group. If you already targeted a resource group, untarget it:
          ```
          ibmcloud target --unset-resource-group
          ```
          {: pre}
        3. Target the cluster.
          ```
          ibmcloud oc cluster config --cluster <cluster_name_or_ID>
          ```
          {: pre}

<br />





## No resources found
{: #rhoks_ts_not_found}
{: troubleshoot}
{: support}

{: tsSymptoms}
When you are running an `oc` command such as `oc get nodes` or `oc get secrets`, you see an error message similar to the following.

```
No resources found.
```
{: screen}

{: tsCauses}
Your OpenShift token is expired. OpenShift token that are generated by using your {{site.data.keyword.cloud_notm}} IAM credentials expire in 24 hours.

{: tsResolve}
Re-authenticate with the OpenShift token by [copying the `oc login` command from the web console](/docs/openshift?topic=openshift-access_cluster#access_public_se) or [creating an API key](/docs/openshift?topic=openshift-access_cluster#access_api_key).

<br />


## VPN server error due to infrastructure credentials
{: #rhoks_ts_openvpn_login}

{: tsSymptoms}
After you create or update a cluster, the master status returns a VPN server configuration error message similar to the following.
```
VPN server configuration update failed. IBM Cloud support has been notified and is working to resolve this issue.
```
{: screen}

{: tsCauses}
The infrastructure credentials that are associated with the resource group that the cluster is created in are missing (such as the API key owner is no longer part of the account) or missing required permissions.

{: tsResolve}
[Complete the troubleshooting guide](/docs/containers?topic=containers-cs_troubleshoot_clusters#cs_credentials) to check and update the infrastructure credentials that are used for the resource group.

<br />



## Feedback, questions, and support
{: #getting_help}
{: troubleshoot}
{: support}

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


