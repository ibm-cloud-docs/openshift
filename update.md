---

copyright:
  years: 2014, 2026
lastupdated: "2026-09-28"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, upgrade, version, update cluster, update worker nodes, update cluster components, update cluster master

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}





# Updating clusters, worker nodes, and cluster components
{: #update}

Keep your cluster secure and supported by updating the master, worker nodes, and cluster components in the correct order. Updating out of sequence can cause version skew failures or unexpected downtime.
{: shortdesc}

Complete updates in the following order:

1. [Update the cluster master](#master).
2. Update your worker nodes — [Classic](#worker_node), [VPC](#vpc_worker_node), or [Satellite](/docs/satellite?topic=satellite-host-update-workers) — depending on your infrastructure type. Not sure which type you have? In the IBM Cloud console, click your cluster and check the **Infrastructure** field on the Overview tab — it shows **Classic**, **VPC**, or **Satellite**.
3. [Update cluster components](#components) such as Fluentd and Ingress ALBs, if you manage them manually.
4. [Update managed add-ons](#addons-update).

## Updating the master
{: #master}


How do I know when to update the master?
:   You are notified in the console, announcements, and the CLI when updates are available. You can also periodically check the [supported versions page](/docs/openshift?topic=openshift-openshift_versions).

How many versions behind the latest can the master be?
:   You can update the API server only to the next version ahead of its current version (`n+1`).




Can my worker nodes run a later version than the master?
:   Your worker nodes can't run a later `major.minor` Kubernetes version than the master. Additionally, your worker nodes can only be one minor version behind the master version (`n-1`). First, [update your master](#update_master) to the latest Kubernetes version. Then, [update the worker nodes](#worker_node) in your cluster.

Worker nodes can run later patch versions than the master, such as patch versions that are specific to worker nodes for security updates.

How are patch updates applied?
:   By default, patch updates for the master are applied automatically over the course of several days, so a master patch version might show up as available before it is applied to your master. The update automation also skips clusters that are in an unhealthy state or have operations currently in progress. Occasionally, IBM might disable automatic updates for a specific master fix pack, such as a patch that is only needed if a master is updated from one minor version to another. In any of these cases, you can check the [{{site.data.keyword.openshiftshort}} version information](/docs/openshift?topic=openshift-openshift_versions) for any potential impact and choose to safely use the `ibmcloud oc cluster master update` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-update-cli) yourself without waiting for the update automation to apply.

Unlike the master, you must update your workers for each patch version.


What happens during the master update?
:   Your master is highly available with three replica master pods. The master pods have a rolling update, during which only one pod is unavailable at a time. Two instances are up and running so that you can access and change the cluster during the update. Your worker nodes, apps, and resources continue to run.

Can I roll back the update?
:   No, you can't roll back a cluster to a previous version after the update process takes place. Be sure to use a test cluster and follow the instructions to address potential issues before you update your production master.

What process can I follow to update the master?
:   The following diagram shows the process that you can take to update your master.

![Master update process diagram](/images/updating-master2.svg){: caption="Updating Kubernetes master process diagram" caption-side="bottom"}
{: #update_master}

### Steps to update the cluster master
{: #master-steps}

Before you begin, make sure that you have the [**Operator** or **Administrator** IAM platform access role](/docs/openshift?topic=openshift-iam-platform-access-roles). If you're unsure of your access role, go to **Manage → Access (IAM) → Users** in the IBM Cloud console, or ask your account administrator.

If a certificate authority (CA) certificate rotation is in progress, the master update is blocked until the rotation completes. Check the status of any in-progress rotation before you begin.
{: important}

To update the {{site.data.keyword.redhat_openshift_notm}} master _major_ or _minor_ version:

1. Review the [{{site.data.keyword.openshiftshort}} version information](/docs/openshift?topic=openshift-openshift_versions) and make any updates marked _Update before master_.
2. Review any [Kubernetes helpful warnings](https://kubernetes.io/blog/2020/09/03/warnings/){: external}, such as deprecation notices.
3. Check the add-ons and plug-ins that are installed in your cluster for any impact that might be caused by updating the cluster version.

    * Checking add-ons
        1. List the add-ons in the cluster.
            ```sh
            ibmcloud oc cluster addon ls --cluster CLUSTER
            ```
            {: pre}

        2. Check the supported {{site.data.keyword.redhat_openshift_notm}} version for each add-on that is installed.
            ```sh
            ibmcloud oc addon-versions
            ```
            {: pre}

        3. If the add-on must be updated to run in the {{site.data.keyword.redhat_openshift_notm}} version that you want to update your cluster to, [update the add-on](/docs/openshift?topic=openshift-managed-addons#updating-managed-add-ons).

    * Checking plug-ins
        1. In the [Helm catalog](https://cloud.ibm.com/kubernetes/helm){: external}, find the plug-ins that you installed in your cluster.
        2. From the side menu, expand the **SOURCES & TAR FILE** section.
        3. Download and open the source code.
        4. Check the `README.md` or `RELEASENOTES.md` files for supported versions.
        5. If the plug-in must be updated to run in the {{site.data.keyword.redhat_openshift_notm}} version that you want to update your cluster to, update the plug-in by following the plug-in instructions.

4. Update your API server and associated master components by using the [{{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/login) or running the CLI `ibmcloud oc cluster master update` [command](/docs/openshift?topic=openshift-kubernetes-service-cli#cluster-master-update-cli).
5. Wait a few minutes, then confirm that the update is complete. Review the API server version on the {{site.data.keyword.cloud_notm}} clusters dashboard or run `ibmcloud oc cluster ls`.
6. Install the version of the [`oc cli`](/docs/openshift?topic=openshift-cli-install) that matches the API server version that runs in the master. Kubernetes does not support `oc` client versions that are two or more versions apart from the server version (n +/- 2). To refresh your local configuration, run `ibmcloud oc cluster config -c CLUSTER_NAME_OR_ID`, then verify with `oc version --client`.

When the master update is complete, update your worker nodes. The method depends on your infrastructure type:
1. [Updating classic worker nodes](#worker_node) — uses a rolling update controlled by a ConfigMap and the `worker update` command.
2. [Updating VPC worker nodes](#vpc_worker_node) — VPC bare metal workers are updated in place using `worker reload`; VPC VSI workers must use `worker replace --update`. The ConfigMap rolling update procedure is not yet supported for VPC worker nodes.



## Updating classic worker nodes
{: #worker_node}

Classic infrastructure worker nodes perform a rolling update in place. Updates are controlled by a Kubernetes ConfigMap that defines how many nodes can be unavailable at one time. The `ibmcloud oc worker update` command is supported only for classic worker nodes.
{: shortdesc}

You can make two types of updates:

* **Patch**: Applies security fixes and updates to the latest patch version. Use `ibmcloud oc worker reload` or `ibmcloud oc worker update`. Both commands update the node to the latest patch version. The `update` command also applies any available `major.minor` version update to match the master at the same time.
* **Major.minor**: Moves the worker node Kubernetes version up to match the master. Your worker nodes can be at most one version behind the master (`n-1`). Use the `ibmcloud oc worker update` command.

For more information, see [Update types](/docs/containers?topic=containers-cs_versions#update_types).

It is good practice to [rotate your CA certificates](/docs/containers?topic=containers-cert-rotate) whenever you update your worker nodes, as the longest step of certificate rotation includes reloading or replacing your worker nodes.
{: tip}

What happens to my apps during an update?
:   Apps that run on updated worker nodes are rescheduled onto other worker nodes in the cluster — including nodes in different worker pools or stand-alone worker nodes. To avoid downtime, make sure that you have enough capacity in the cluster to carry the workload before you start the update.

How can I control how many worker nodes go down at a time during an update or reload?
:   Use a Kubernetes ConfigMap to set the maximum number of worker nodes that can be unavailable at a time. Worker nodes are identified by their labels. You can use IBM-provided labels or custom labels. If you need all your worker nodes to remain available, consider [resizing your worker pool](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-pool-resize-cli) or [adding stand-alone worker nodes](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-pool-create-classic-cli) to add temporary capacity before the update.

The ConfigMap controls update behavior only. It does not affect worker node reloads, which happen immediately when requested.
{: important}

What if I choose not to define a config map?
:   By default, a maximum of 20% of all worker nodes in each cluster can be unavailable during the update. You can override this value by defining a ConfigMap with a `defaultcheck.json` entry.

### Prerequisites
{: #worker-up-prereqs}

Before you update your classic infrastructure worker nodes, complete the following prerequisite steps.
{: shortdesc}

During a worker node update, the worker node machine is reimaged and all data that is not [stored on persistent storage](/docs/openshift?topic=openshift-storage-plan) is permanently deleted. Verify that any data you need to retain is stored outside the worker node before you begin.
{: important}

If you have Portworx installed in your cluster, you must [update your Portworx configuration before you update worker nodes](/docs/openshift?topic=openshift-storage_portworx_plan#portworx_limitations).
{: important}

#### Pre-update actions (complete in order)
{: #classic-worker-prereq-actions}

1. Review the [{{site.data.keyword.openshiftshort}} version information](/docs/openshift?topic=openshift-openshift_versions) for the latest security patches and required changes.
2. Make any changes that are marked with _Update before master_ or _Update after master_ in the [{{site.data.keyword.redhat_openshift_notm}} version preparation guide](/docs/openshift?topic=openshift-openshift_versions).
3. [Update the master](#master) before updating worker nodes. The worker node version cannot be higher than the API server version that runs in the master.
4. [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).
5. Consider [adding worker nodes](/docs/openshift?topic=openshift-add-workers-classic) to your cluster to provide extra capacity for workload rescheduling during the update. You can remove the extra nodes after the update is complete.

#### Required permissions
{: #classic-worker-prereq-perms}

Make sure that you have the [**Operator** or **Administrator** IAM platform access role](/docs/openshift?topic=openshift-iam-platform-access-roles). If you're unsure of your access role, go to **Manage → Access (IAM) → Users** in the IBM Cloud console, or ask your account administrator.

### Updating classic worker nodes in the CLI with a configmap
{: #worker-up-configmap}

Use a ConfigMap to perform a rolling update of your classic worker nodes. The ConfigMap lets you control how many nodes can be unavailable at a time, per zone or region. If the default 20% unavailability rule is acceptable for your cluster, you can skip steps 3 and 4 (ConfigMap creation) and proceed directly to step 5 to apply the update using the default behavior.
{: shortdesc}

1. Complete the [prerequisite steps](#worker-up-prereqs).
2. List available worker nodes and note their private IP address.

    ```sh
    ibmcloud oc worker ls --cluster CLUSTER
    ```
    {: pre}

3. View the labels of a worker node. You can find the worker node labels in the **Labels** section of your CLI output. Every label consists of a `NodeSelectorKey` and a `NodeSelectorValue`.
    ```sh
    oc describe node PRIVATE-WORKER-IP
    ```
    {: pre}

    Example output

    ```sh
    NAME:               10.184.58.3
    Roles:              <none>
    Labels:             arch=amd64
                    beta.kubernetes.io/arch=amd64
                    beta.kubernetes.io/os=linux
                    failure-domain.beta.kubernetes.io/region=us-south
                    failure-domain.beta.kubernetes.io/zone=dal12
                    ibm-cloud.kubernetes.io/encrypted-docker-data=true
                    ibm-cloud.kubernetes.io/iaas-provider=softlayer
                    ibm-cloud.kubernetes.io/machine-type=u3c.2x4.encrypted
                    kubernetes.io/hostname=10.123.45.3
                    privateVLAN=2299001
                    publicVLAN=2299012
    Annotations:        node.alpha.kubernetes.io/ttl=0
                    volumes.kubernetes.io/controller-managed-attach-detach=true
    CreationTimestamp:  Tue, 03 Apr 2022 15:26:17 -0400
    Taints:             <none>
    Unschedulable:      false
    ```
    {: screen}

4. Create a config map and define the unavailability rules for your worker nodes. The ConfigMap supports up to 15 named checks. Each check targets a set of worker nodes by label and sets the maximum percentage of those nodes that can be unavailable at one time. The following example shows a zone check (`zonecheck.json`), a region check (`regioncheck.json`), a default fallback check (`defaultcheck.json`), and a template for custom checks. For every check, choose one of the worker node labels that you retrieved in the previous step to identify the target nodes.

    For every check, you can set only one value for `NodeSelectorKey` and `NodeSelectorValue`. If you want to set rules for more than one region, zone, or other worker node labels, create a new check. Define up to 15 checks in a config map. If you add more checks, only 1 worker node is reloaded at a time until all workers requested are updated.
    {: note}

    Example
    ```yaml
    apiVersion: v1
    kind: ConfigMap
    metadata:
      name: ibm-cluster-update-configuration
      namespace: kube-system
    data:
      drain_timeout_seconds: "120"
      zonecheck.json: |
        {
          "MaxUnavailablePercentage": 30,
          "NodeSelectorKey": "failure-domain.beta.kubernetes.io/zone",
          "NodeSelectorValue": "dal13"
        }
      regioncheck.json: |
        {
          "MaxUnavailablePercentage": 20,
          "NodeSelectorKey": "failure-domain.beta.kubernetes.io/region",
          "NodeSelectorValue": "us-south"
        }
      defaultcheck.json: |
        {
          "MaxUnavailablePercentage": 20
        }
      <check_name>: |
        {
          "MaxUnavailablePercentage": <value_in_percentage>,
          "NodeSelectorKey": "<node_selector_key>",
          "NodeSelectorValue": "<node_selector_value>"
        }
    ```
    {: codeblock}

    `drain_timeout_seconds`
    :    Optional: The timeout in seconds to wait for the [drain](https://kubernetes.io/docs/tasks/administer-cluster/safely-drain-node/){: external} to complete. Draining a worker node safely removes all existing pods from the worker node and reschedules the pods onto other worker nodes in the cluster. Accepted values are integers in the range 1 - 180. The default value is 30.

    `zonecheck.json` and `regioncheck.json`
    :   Two checks that define a rule for a set of worker nodes that you can identify with the specified `NodeSelectorKey` and `NodeSelectorValue`. The `zonecheck.json` identifies worker nodes based on their zone label, and the `regioncheck.json` uses the region label that is added to every worker node during provisioning. In the example, 30% of all worker nodes that have `dal13` as their zone label and 20% of all the worker nodes in `us-south` can be unavailable during the update.

    `defaultcheck.json`
    :   If you don't create a config map or the map is configured incorrectly, the Kubernetes default is applied. By default, only 20% of the worker nodes in the cluster can be unavailable at a time. You can override the default value by adding the default check to your config map. In the example, every worker node that is not specified in the zone and region checks (`dal13` or `us-south`) can be unavailable during the update. 

    `MaxUnavailablePercentage`
    :   The maximum number of nodes that are allowed to be unavailable for a specified label key and value, which is specified as a percentage. A worker node is unavailable during the deploying, reloading, or provisioning process. The queued worker nodes are blocked from updating if it exceeds any defined maximum unavailable percentages. 

    `NodeSelectorKey`
    :   The label key of the worker node for which you want to set a rule. You can set rules for the default labels that are provided by IBM, as well as on worker node labels that you created. If you want to add a rule for worker nodes that belong to one worker pool, you can use the `ibm-cloud.kubernetes.io/machine-type` label.

    `NodeSelectorValue`
    :   The label value that the worker node must have to be considered for the rule that you define.
        
5. Create the configuration map in your cluster.
    ```sh
    oc apply -f <filepath/configmap.yaml>
    ```
    {: pre}

6. Verify that the config map is created.
    ```sh
    oc get configmap --namespace kube-system
    ```
    {: pre}

7. Update the worker nodes.

    ```sh
    ibmcloud oc worker update --cluster CLUSTER --worker WORKER-NODE-1-ID --worker WORKER-NODE-2-ID
    ```
    {: pre}

8. Optional: Verify the events that are triggered by the config map and any validation errors that occur. The events can be reviewed in the  **Events** section of your CLI output.
    ```sh
    oc describe -n kube-system cm ibm-cluster-update-configuration
    ```
    {: pre}

9. Confirm that the update is complete by reviewing the Kubernetes version of your worker nodes.  
    ```sh
    oc get nodes
    ```
    {: pre}

10. Verify that you don't have duplicate worker nodes. Sometimes, older clusters list duplicate worker nodes with a **`NotReady`** status after an update. To remove duplicates, see [troubleshooting](/docs/openshift?topic=openshift-cs_duplicate_nodes).

#### Next steps
{: #classic-worker-next-steps}

1. Repeat the update process with other worker pools.
2. Notify all developers who work in the cluster to [update their `oc` CLI](/docs/openshift?topic=openshift-cli-install) to match the Kubernetes master version. Running a `oc` client that is two or more versions apart from the server version is not supported and can cause unexpected errors.
{: important}

3. If the Kubernetes dashboard does not display utilization graphs, [delete the `kube-dashboard` pod](/docs/containers?topic=containers-cs_dashboard_graphs).

### Updating classic worker nodes in the console
{: #worker_up_console}

After you set up the ConfigMap for the first time, you can update worker nodes by using the {{site.data.keyword.cloud_notm}} console. The console respects the unavailability rules that you defined in the ConfigMap.
{: shortdesc}

1. Complete the [prerequisite steps](#worker-up-prereqs) and [set up a ConfigMap](#worker-up-configmap) to control how your worker nodes are updated.
2. From the [{{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/) menu ![Menu icon](../icons/icon_hamburger.svg "Menu icon"), click **Containers** > **Clusters**.
3. From the **Clusters** page, click your cluster.
4. From the **Worker Nodes** tab, select the checkbox for each worker node that you want to update. An action bar is displayed over the table header row.
5. From the action bar, click **Update**.

If you have Portworx installed in your cluster, you must restart the Portworx pods on the updated worker nodes. For more information, see [Portworx limitations](/docs/openshift?topic=openshift-storage_portworx_plan#portworx_limitations).
{: important}



## Updating VPC worker nodes
{: #vpc_worker_node}

VPC worker nodes are updated differently depending on their type and cluster platform. The `ibmcloud oc worker update` command is not supported for any VPC worker node. In all cases, the cluster master must be updated first.
{: shortdesc}


- **VPC bare metal workers**: Updated in place using `ibmcloud oc worker reload`. The node retains its IP address.
- **VPC virtual server instance (VSI) workers**: Replaced using `ibmcloud oc worker replace --update` (to match the master version) or `ibmcloud oc worker replace` (patch refresh only). The old node is deleted and a new one is provisioned.



You can make two types of updates:

* **Patch**: Applies security fixes and updates to the latest patch of the current BOM version. For VPC bare metal workers, use `ibmcloud oc worker reload`. For VPC VSI workers, use `ibmcloud oc worker replace`.
* **Major.minor**: Moves the worker node Kubernetes version up to match the master. Your worker nodes can be at most one version behind the master (`n-1`). For VPC bare metal workers, use `ibmcloud oc worker reload`. For VPC VSI workers, use `ibmcloud oc worker replace --update`.

It is good practice to [rotate your CA certificates](/docs/containers?topic=containers-cert-rotate) whenever you update your worker nodes, as the longest step of certificate rotation includes reloading or replacing your worker nodes.
{: tip}



If you have OpenShift Data Foundation deployed in your cluster, follow the steps to [update VPC worker nodes with OpenShift Data Foundation](/docs/openshift?topic=openshift-openshift-storage-update-vpc).
{: important}



What happens to my apps during an update?
:   Apps that run on updated worker nodes are rescheduled onto other worker nodes in the cluster. These worker nodes might be in a different worker pool. To avoid downtime, make sure that you have enough capacity in your cluster to carry the workload before you start the update. For more information, see [Adding worker nodes to Classic clusters](/docs/openshift?topic=openshift-add-workers-classic) or [Adding worker nodes to VPC clusters](/docs/openshift?topic=openshift-add-workers-vpc).

What happens to my worker node during an update?
:   For VPC bare metal workers, the worker node is reloaded in place using `worker reload`. The node retains its IP address; data on local disks is deleted and must be stored outside the worker node. For VPC virtual server instance (VSI) workers, the worker node is replaced by removing the old worker node and provisioning a new worker node that runs at the updated patch or `major.minor` version. The replacement worker node is created in the same zone, same worker pool, and with the same flavor as the deleted worker node. However, the replacement worker node is assigned a new private IP address, and loses any custom labels or taints that you applied to the old worker node (worker pool labels and taints are still applied to the replacement worker node).

What if I replace multiple worker nodes at the same time?
:   If you replace multiple worker nodes at the same time, they are deleted and replaced concurrently, not one by one. Make sure that you have enough capacity in your cluster to reschedule your workloads before you replace worker nodes.

What if a replacement worker node is not created?
:   A replacement worker node is not created if the worker pool does not have [automatic rebalancing enabled](/docs/openshift?topic=openshift-auto-rebalance-off).

### Prerequisites
{: #vpc_worker_prereqs}

Before you update your VPC infrastructure worker nodes, complete the following prerequisite steps.
{: shortdesc}

For VPC VSI workers, the worker node is deleted and replaced with a new node. For VPC bare metal workers, the node is reloaded in place. In both cases, data that is not [stored on persistent storage](/docs/openshift?topic=openshift-storage-plan) is permanently deleted. Verify that any data you need to retain is stored outside the worker node before you begin.
{: important}

If you have Portworx deployed in your cluster, follow the steps to [update VPC worker nodes with Portworx volumes](/docs/openshift?topic=openshift-storage_portworx_update#portworx_vpc_up) instead of the steps on this page.
{: important}

#### Pre-update actions (complete in order)
{: #vpc-worker-prereq-actions}

1. Review the [{{site.data.keyword.openshiftshort}} version information](/docs/openshift?topic=openshift-openshift_versions) for the latest security patches and required changes.
2. Make any changes that are marked with _Update before master_ or _Update after master_ in the [{{site.data.keyword.redhat_openshift_notm}} version preparation guide](/docs/openshift?topic=openshift-openshift_versions).
3. [Update the master](#master) before updating worker nodes. The worker node version cannot be higher than the API server version that runs in the master.
4. [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).

#### Required permissions
{: #vpc-worker-prereq-perms}

Make sure that you have the [**Operator** or **Administrator** IAM platform access role](/docs/openshift?topic=openshift-iam-platform-access-roles). If you're unsure of your access role, go to **Manage → Access (IAM) → Users** in the IBM Cloud console, or ask your account administrator.

### Updating VPC worker nodes in the CLI
{: #vpc_worker_cli}
{: cli}

Complete the following steps to update your worker nodes by using the CLI.
{: shortdesc}

1. Complete the [prerequisite steps](#vpc_worker_prereqs).
2. Optional: Add capacity to your cluster by resizing the worker pool. The pods on the worker node can be rescheduled and continue running on the added worker nodes during the update. For more information, see [Adding worker nodes to Classic clusters](/docs/openshift?topic=openshift-add-workers-classic) or [Adding worker nodes to VPC clusters](/docs/openshift?topic=openshift-add-workers-vpc).
3. List the worker nodes in your cluster and note the **ID** and **Primary IP** of the worker node that you want to update.
    ```sh
    ibmcloud oc worker ls --cluster CLUSTER
    ```
    {: pre}

4. Update the worker node. The command to use depends on the worker node type.

    **VPC bare metal workers**: Use `worker reload` to reimage the node in place. The node retains its IP address and is updated to the latest patch version.

    ```sh
    ibmcloud oc worker reload --cluster CLUSTER --worker WORKER-NODE-ID
    ```
    {: pre}

    **VPC virtual server instance (VSI) workers**: Use the `worker replace` command to update either the patch version or the `major.minor` version that matches the master version.

    *  To update the worker node to the same `major.minor` version as the master, include the `--update` option.
        ```sh
        ibmcloud oc worker replace --cluster CLUSTER --worker WORKER-NODE-ID --update
        ```
        {: pre}

    *  To update the worker node to the latest patch version at the same `major.minor` version, don't include the `--update` option.
        ```sh
        ibmcloud oc worker replace --cluster CLUSTER --worker WORKER-NODE-ID
        ```
        {: pre}

5. Repeat these steps for each worker node that you must update.
6. Optional: After the replaced worker nodes are in a **Ready** status, resize the worker pool to meet the cluster capacity that you want. For more information, [Adding worker nodes to VPC clusters](/docs/openshift?topic=openshift-add-workers-vpc).

If you are running Portworx in your VPC cluster, you must [manually attach your {{site.data.keyword.block_storage_is_short}} volume to your new worker node.](/docs/openshift?topic=openshift-storage_portworx_update)
{: note}

### Firmware updates during VPC bare metal worker reload
{: #vpc_bm_firmware}

When you reload a VPC bare metal worker node, {{site.data.keyword.cloud_notm}} infrastructure automatically checks whether a firmware update is pending for that server and applies it as part of the reload process. No additional action is required to trigger the firmware update.

Be aware of the following considerations when you reload a VPC bare metal worker node:

Extended reload time
:   If a firmware update is applied during the reload, the total reload time can increase significantly — by 30 minutes or more — beyond the typical reload duration. Plan your maintenance windows accordingly.

No advance visibility into pending updates
:   There is no visibility into whether a firmware update is pending for a worker node before you issue the reload command.

Data loss risk
:   As with all VPC bare metal worker reloads, data on local disks is deleted during the reload regardless of whether a firmware update is applied. Back up any data that is not stored on persistent storage before you reload.

Reload failure due to firmware update
:   In some cases, a firmware update can fail, which causes the worker node to enter a `reload_failed` state (`Failed to reload worker`) with status detail `The infrastructure firmware update has failed. (P4056)`. If this occurs:
    1. Wait a few minutes, then retry the reload by running `ibmcloud oc worker reload --cluster CLUSTER --worker WORKER-NODE-ID` again.
    2. If the error persists after 2–3 attempts, open an [{{site.data.keyword.cloud_notm}} support case](/docs/openshift?topic=openshift-get-help).


### Updating VPC worker nodes in the console
{: #vpc_worker_ui}
{: ui}

You can update your VPC worker nodes in the console. Before you begin, consider [adding worker nodes](/docs/openshift?topic=openshift-add-workers-vpc) to the cluster to help avoid downtime for your apps.
{: shortdesc}

What the **Update** action does depends on the worker node type and cluster platform:
- **VPC bare metal workers**: The node is reloaded in place. No replacement node is provisioned.
- **VPC virtual server instance (VSI) workers**: The worker node is replaced with a new node at the updated version.


1. Complete the [prerequisite steps](#vpc_worker_prereqs).
2. From the [{{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/) menu ![Menu icon](../icons/icon_hamburger.svg "Menu icon"), click **Containers** > **Clusters**.
3. From the **Clusters** page, click your cluster.
4. From the **Worker Nodes** tab, select the checkbox for each worker node that you want to update. An action bar is displayed over the table header row.
5. From the action bar, click **Update**.



## Updating flavors (machine types)
{: #machine_type}

Update the flavor (machine type) of your worker nodes when you need different compute resources — for example, more memory, additional CPUs, or a GPU-enabled machine. Updating a flavor provisions a new worker pool with the new flavor and then removes the old worker pool. Because this process replaces nodes, all data on the worker nodes that is not stored on persistent storage is permanently deleted.
{: shortdesc}

#### Before you begin
{: #machine-type-prereqs}

- [Access your {{site.data.keyword.redhat_openshift_notm}} cluster](/docs/openshift?topic=openshift-access_cluster).
- Verify that any data you need to retain is stored on [persistent storage](/docs/openshift?topic=openshift-storage-plan) outside the worker node. Data stored only on the worker node is lost and cannot be recovered.
- Make sure that you have the [**Operator** or **Administrator** IAM platform access role](/docs/openshift?topic=openshift-iam-platform-access-roles). If you're unsure of your access role, go to **Manage → Access (IAM) → Users** in the IBM Cloud console, or ask your account administrator.

#### To update flavors
{: #machine-type-steps}

1. List available worker nodes and note their private IP address.

    1. List available worker pools in your cluster.
        ```sh
        ibmcloud oc worker-pool ls --cluster CLUSTER
        ```
        {: pre}

    2. List the worker nodes in the worker pool. Note the **ID** and **Private IP**.
        ```sh
        ibmcloud oc worker ls --cluster CLUSTER --worker-pool WORKER-POOL
        ```
        {: pre}

    3. Get the details for a worker node. In the output, note the zone and either the private and public VLAN ID for classic clusters or the subnet ID for VPC clusters.
        ```sh
        ibmcloud oc worker get --cluster CLUSTER --worker WORKER-ID
        ```
        {: pre}

2. List available flavors in the zone.
    ```sh
    ibmcloud oc flavors --zone <zone>
    ```
    {: pre}

3. Create a worker node with the new machine type.
    1. Create a worker pool with the number of worker nodes that you want to replace.
        * Classic clusters:
            ```sh
            ibmcloud oc worker-pool create classic --name WORKER-POOL --cluster CLUSTER --flavor FLAVOR --size-per-zone NUMBER-OF-WORKERS-PER-ZONE
            ```
            {: pre}

        * VPC Generation 2 clusters:
            ```sh
            ibmcloud oc worker-pool create vpc-gen2 --name NAME --cluster CLUSTER --flavor FLAVOR --size-per-zone NUMBER-OF-WORKERS-PER-ZONE --label LABEL
            ```
            {: pre}

    2. Verify that the worker pool is created.
        ```sh
        ibmcloud oc worker-pool ls --cluster CLUSTER
        ```
        {: pre}

    3. Add the zone to your worker pool that you retrieved earlier. When you add a zone, the worker nodes that are defined in your worker pool are provisioned in the zone and considered for future workload scheduling. If you want to spread your worker nodes across multiple zones, choose a [classic](/docs/openshift?topic=openshift-regions-and-zones#zones-mz) or [VPC](/docs/openshift?topic=openshift-regions-and-zones#zones-vpc) multizone location.
        * Classic clusters:
            ```sh
            ibmcloud oc zone add classic --zone ZONE --cluster CLUSTER --worker-pool WORKER-POOL --private-vlan PRIVATE-VLAN-ID --public-vlan PUBLIC-VLAN-ID
            ```
            {: pre}

        * VPC clusters:
            ```sh
            ibmcloud oc zone add vpc-gen2 --zone ZONE --cluster CLUSTER --worker-pool WORKER-POOL --subnet-id VPC-SUBNET-ID
            ```
            {: pre}

4. Wait for the worker nodes to be deployed. When the worker node state changes to **Normal**, the deployment is finished.
    ```sh
    ibmcloud oc worker ls --cluster CLUSTER
    ```
    {: pre}

5. Remove the old worker pool. If you are removing a Classic bare metal flavor (which is billed monthly), you are charged for the entire month even if you remove it mid-month. VPC workers, including bare metal, are billed hourly.
{: important}

    1. Remove the worker pool with the old machine type. Removing a worker pool removes all worker nodes in the pool in all zones. This process might take a few minutes to complete.
        ```sh
        ibmcloud oc worker-pool rm --worker-pool WORKER-POOL --cluster CLUSTER
        ```
        {: pre}

    2. Verify that the worker pool is removed.
        ```sh
        ibmcloud oc worker-pool ls --cluster CLUSTER
        ```
        {: pre}

6. Verify that the worker nodes are removed from your cluster.
    ```sh
    ibmcloud oc worker ls --cluster CLUSTER
    ```
    {: pre}

7. Repeat these steps to update other worker pools or stand-alone worker nodes to different flavors.

## How are worker pools scaled down?
{: #worker-scaledown-logic}

This section describes the automatic prioritization logic used when worker nodes are removed during a scale-down, such as after a worker node update or when you run [`ibmcloud oc worker-pool resize`](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-pool-resize-cli). You do not need to configure this behavior — it happens automatically.

When the number of worker nodes in a worker pool is decreased, the worker nodes are prioritized for deletion based on several properties including state, health, and version.

This priority logic is not relevant to the autoscaler add-on.
{: note}

The following table shows the order in which worker nodes are prioritized for deletion.

You can run the `ibmcloud oc worker ls` command to view all the worker node properties listed in the table. 
{: tip}

| Priority | Property | Description |
|---|---|---|
| 1 | Worker node state | Worker nodes in non-functioning or low-functioning states are prioritized for removal. This list shows the states ordered from highest to lowest priority: `provision_failed`, `deploy_failed`, `deleting`, `provision_pending`, `provisioning`, `deploying`, `provisioned`, `reloading_failed`, `reloading`, `deployed`. |
| 2 | Worker node health | Unhealthy worker nodes are prioritized over healthy worker nodes. This list shows the health states ordered from highest to lowest priority: `critical`, `warning`, `pending`, `unsupported`, `normal`.|
| 3 | Worker node version | Worker nodes that run on older versions are at a higher priority for deletion. |
| 4 | Chosen placement setting | **For workers running on a dedicated host only.** Worker nodes running on a dedicated host that has the `DesiredPlacementDisabled` option set to `true` are at a higher priority for deletion. | 
| 5 | Alphabetical order | After worker nodes are prioritized based on the factors listed above, they are deleted in alphabetical order. Note that, based on worker node ID conventions, IDs for workers on classic and VPC clusters correlate with age, so older worker nodes are removed first. |
{: caption="Priority for worker nodes deleted during worker pool scale down." caption-side="bottom"}



## Updating cluster components
{: #components}

Your {{site.data.keyword.openshiftlong_notm}} cluster comes with components, such as Ingress, that are installed automatically when you provision the cluster. By default, these components are updated automatically by IBM. However, you can disable automatic updates for some components and manually update them separately from the master and worker nodes.
{: shortdesc}

What default components can I update separately from the cluster?
:   You can optionally disable automatic updates for the following components:
    * [Fluentd for logging](#logging-up)
    * [Ingress application load balancer (ALB)](#alb)

Are there components that I can't update separately from the cluster?
:   Yes. Your cluster is deployed with the following managed components and associated resources that can't be changed, except to scale pods or edit configmaps for certain performance benefits. If you try to change one of these deployment components, their original settings are restored on a regular interval when they are updated with the cluster master. However, note that resources that you create that are associated with these components, such as Calico network policies that you create to be implemented by the Calico deployment components, are not updated.

* `calico` components
* `coredns` components
* `ibm-cloud-provider-ip`
* `ibm-file-plugin`
* `ibm-keepalived-watcher`
* `ibm-master-proxy`
* `ibm-storage-watcher`
* `kubernetes-dashboard` components
* `metrics-server`
* `olm-operator` and `catalog` components (1.16 and later)
* `vpn`

Can I install other plug-ins or add-ons than the default components?
:   Yes. {{site.data.keyword.openshiftlong_notm}} provides other plug-ins and add-ons that you can choose from to add capabilities to your cluster. For example, you might want to enable IBM-managed add-ons in your cluster. You must update these add-ons separately by following the steps to [update managed add-ons](/docs/openshift?topic=openshift-managed-addons#updating-managed-add-ons).

### Managing automatic updates for Fluentd
{: #logging-up}

When you create a logging configuration for a source in your cluster to forward to an external server, a Fluentd component is created in your cluster. To change your logging or filter configurations, the Fluentd component must be at the latest version. By default, automatic updates to the component are enabled.
{: shortdesc}

To run the following commands, you must have the [**Administrator** {{site.data.keyword.cloud_notm}} IAM platform access role](/docs/openshift?topic=openshift-iam-platform-access-roles) for the cluster.

You can manage automatic updates of the Fluentd component in the following ways.

* Check whether automatic updates are enabled by running the `ibmcloud oc logging autoupdate get --cluster CLUSTER` [command](/docs/containers?topic=containers-kubernetes-service-cli#logging-autoupdate-get-cli).
* Disable automatic updates by running the `ibmcloud oc logging autoupdate disable` [command](/docs/containers?topic=containers-kubernetes-service-cli#logging-autoupdate-disable-cli).
* If automatic updates are disabled, but you need to change your configuration, you have two options:
    * Turn on automatic updates for your Fluentd pods.
        ```sh
        ibmcloud oc logging autoupdate enable --cluster CLUSTER
        ```
        {: pre}

    * Force a one-time update when you use a logging command that includes the `--force-update` option. Your pods update to the latest version of the Fluentd component, but Fluentd does not update automatically going forward.
        Example command

        ```sh
        ibmcloud oc logging config update --cluster CLUSTER --id LOG-CONFIG-ID --type LOG-TYPE --force-update
        ```
        {: pre}

### Managing automatic updates for Ingress ALBs
{: #alb}

Control when the Ingress application load balancer (ALB) component is updated. For information about keeping ALBs up-to-date, see [Managing the Ingress ALB lifecycle](/docs/openshift?topic=openshift-ingress-about-roks4).
{: shortdesc}



## Updating managed add-ons
{: #addons-update}

Managed {{site.data.keyword.containerlong_notm}} cluster add-ons are an easy way to enhance your cluster with open-source capabilities, such as Istio. The version of the open-source tool that you add to your cluster is tested by IBM and approved for use in {{site.data.keyword.containerlong_notm}}. To update managed add-ons that you enabled in your cluster to the latest versions, see [Updating managed add-ons](/docs/openshift?topic=openshift-managed-addons#updating-managed-add-ons).
