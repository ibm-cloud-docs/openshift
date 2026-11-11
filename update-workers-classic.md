---

copyright:
  years: 2026, 2026
lastupdated: "2026-11-10"


keywords: openshift, {{site.data.keyword.openshiftlong_notm}}, update classic worker nodes, worker update, configmap, rolling update

subcollection: openshift

content-type: howto

---

{{site.data.keyword.attribute-definition-list}}


# Updating classic worker nodes
{: #update-workers-classic}

Classic infrastructure worker nodes perform a rolling update in place. Updates are controlled by a Kubernetes ConfigMap that defines how many nodes can be unavailable at one time. The `ibmcloud oc worker update` command is supported only for classic worker nodes.
{: shortdesc}

## How classic worker node updates work
{: #classic-worker-faq}

You can make two types of updates:

* **Patch**: Applies security fixes and updates to the latest patch version. Use `ibmcloud oc worker reload` or `ibmcloud oc worker update`. Both commands update the node to the latest patch version. The `update` command also applies any available `major.minor` version update to match the master at the same time.
* **Major.minor**: Moves the worker node Kubernetes version up to match the master. Your worker nodes can be at most one version behind the master (`n-1`). Use the `ibmcloud oc worker update` command.

For more information, see [Update types](/docs/openshift?topic=openshift-openshift_versions#update-types).

What happens to my apps during an update?
:   Apps that run on updated worker nodes are rescheduled onto other worker nodes in the cluster, including nodes in different worker pools or stand-alone worker nodes. To avoid downtime, make sure that you have enough capacity in the cluster to carry the workload before you start the update.

How can I control how many worker nodes go down at a time during an update or reload?
:   Use a Kubernetes ConfigMap to set the maximum number of worker nodes that can be unavailable at a time. Worker nodes are identified by their labels. You can use IBM-provided labels or custom labels. If you need all your worker nodes to remain available, consider [resizing your worker pool](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-pool-resize-cli) or [adding stand-alone worker nodes](/docs/openshift?topic=openshift-kubernetes-service-cli#worker-pool-create-classic-cli) to add temporary capacity before the update.

The ConfigMap controls update behavior only. It does not affect worker node reloads, which happen immediately when requested.
{: important}

What if I choose not to define a ConfigMap?
:   By default, a maximum of 20% of all worker nodes in each cluster can be unavailable during the update. You can override this value by defining a ConfigMap with a `defaultcheck.json` entry.

## Prerequisites
{: #worker-up-prereqs}

Before you update your classic infrastructure worker nodes, complete the following prerequisite steps.
{: shortdesc}

During a worker node update, the worker node machine is reimaged and all data that is not [stored on persistent storage](/docs/openshift?topic=openshift-storage-plan) is permanently deleted. Verify that any data you need to retain is stored outside the worker node before you begin.
{: important}

Also consider the following storage cases before you update.

* If you have Portworx installed in your cluster, review the [Portworx limitations](/docs/openshift?topic=openshift-storage_portworx_plan#portworx_limitations) before you update worker nodes. After the update, if you added raw block storage to the updated worker nodes, restart the Portworx pods on those nodes so that your storage volumes are detected.

* If you have OpenShift Data Foundation deployed in your cluster, follow the steps to [update Classic worker nodes with OpenShift Data Foundation](/docs/openshift?topic=openshift-openshift-storage-update-classic) instead of the steps on this page.


1. Complete the steps in [Preparing to update your cluster](/docs/openshift?topic=openshift-update-prepare).
2. [Update the master](/docs/openshift?topic=openshift-update-master). The worker node version can't be higher than the API server version that runs in the master.
3. Consider [adding worker nodes](/docs/openshift?topic=openshift-add-workers-classic) to your cluster to provide extra capacity for workload rescheduling during the update. You can remove the extra nodes after the update is complete.

## Updating classic worker nodes in the CLI with a ConfigMap
{: #worker-up-configmap}
{: cli}

Use a ConfigMap to perform a rolling update of your classic worker nodes. The ConfigMap lets you control how many nodes can be unavailable at a time, per zone or region. If the default 20% unavailability rule is acceptable for your cluster, you can skip steps 3 through 6 (ConfigMap creation and apply) and proceed directly to step 7 to update the worker nodes by using the default behavior.
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

4. Create a ConfigMap and define the unavailability rules for your worker nodes. The ConfigMap supports up to 15 named checks. Each check targets a set of worker nodes by label and sets the maximum percentage of those nodes that can be unavailable at one time. The following example shows a zone check (`zonecheck.json`), a region check (`regioncheck.json`), a default fallback check (`defaultcheck.json`), and a template for custom checks. For every check, choose one of the worker node labels that you retrieved in the previous step to identify the target nodes.

    For every check, you can set only one value for `NodeSelectorKey` and `NodeSelectorValue`. If you want to set rules for more than one region, zone, or other worker node labels, create a new check. Define up to 15 checks in a ConfigMap. If you add more checks, only 1 worker node is reloaded at a time until all workers requested are updated.
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
      CHECK_NAME: |
        {
          "MaxUnavailablePercentage": VALUE_IN_PERCENTAGE,
          "NodeSelectorKey": "NODE_SELECTOR_KEY",
          "NodeSelectorValue": "NODE_SELECTOR_VALUE"
        }
    ```
    {: codeblock}

    `drain_timeout_seconds`
    :    Optional: The timeout in seconds to wait for the [drain](https://kubernetes.io/docs/tasks/administer-cluster/safely-drain-node/){: external} to complete. Draining a worker node safely removes all existing pods from the worker node and reschedules the pods onto other worker nodes in the cluster. Accepted values are integers in the range 1 - 180. The default value is 30.

    `zonecheck.json` and `regioncheck.json`
    :   Two checks that define a rule for a set of worker nodes that you can identify with the specified `NodeSelectorKey` and `NodeSelectorValue`. The `zonecheck.json` identifies worker nodes based on their zone label, and the `regioncheck.json` uses the region label that is added to every worker node during provisioning. In the example, 30% of all worker nodes that have `dal13` as their zone label and 20% of all the worker nodes in `us-south` can be unavailable during the update.

    `defaultcheck.json`
    :   If you don't create a ConfigMap or the ConfigMap is configured incorrectly, the Kubernetes default is applied. By default, only 20% of the worker nodes in the cluster can be unavailable at a time. You can override the default value by adding the default check to your ConfigMap. In the example, every worker node that is not specified in the zone and region checks (`dal13` or `us-south`) can be unavailable during the update. 

    `MaxUnavailablePercentage`
    :   The maximum number of nodes that are allowed to be unavailable for a specified label key and value, which is specified as a percentage. A worker node is unavailable during the deploying, reloading, or provisioning process. The queued worker nodes are blocked from updating if it exceeds any defined maximum unavailable percentages. 

    `NodeSelectorKey`
    :   The label key of the worker node for which you want to set a rule. You can set rules for the default labels that are provided by IBM, as well as on worker node labels that you created. If you want to add a rule for worker nodes that belong to one worker pool, you can use the `ibm-cloud.kubernetes.io/machine-type` label.

    `NodeSelectorValue`
    :   The label value that the worker node must have to be considered for the rule that you define.
        
5. Create the configuration map in your cluster.
    ```sh
    oc apply -f CONFIGMAP_FILE_PATH
    ```
    {: pre}

6. Verify that the ConfigMap is created.
    ```sh
    oc get configmap --namespace kube-system
    ```
    {: pre}

7. Update the worker nodes.

    ```sh
    ibmcloud oc worker update --cluster CLUSTER --worker WORKER-NODE-1-ID --worker WORKER-NODE-2-ID
    ```
    {: pre}

8. Optional: Verify the events that are triggered by the ConfigMap and any validation errors that occur. The events can be reviewed in the  **Events** section of your CLI output.
    ```sh
    oc describe -n kube-system cm ibm-cluster-update-configuration
    ```
    {: pre}

9. Confirm that the update is complete by reviewing the Kubernetes version of your worker nodes. For worker node states, see [Worker node states](/docs/openshift?topic=openshift-worker-node-state-reference).  
    ```sh
    oc get nodes
    ```
    {: pre}

10. Verify that you don't have duplicate worker nodes. Sometimes, older clusters list duplicate worker nodes with a **`NotReady`** status after an update. To remove duplicates, see [troubleshooting](/docs/openshift?topic=openshift-cs_duplicate_nodes).

## Updating classic worker nodes in the console
{: #worker-up-console}
{: ui}

After you set up the ConfigMap for the first time, you can update worker nodes by using the {{site.data.keyword.cloud_notm}} console. The console respects the unavailability rules that you defined in the ConfigMap.
{: shortdesc}

1. Complete the [prerequisite steps](#worker-up-prereqs) and [set up a ConfigMap](/docs/containers?topic=containers-update-workers-classic&interface=cli#worker-up-configmap) to control how your worker nodes are updated.
2. From the [{{site.data.keyword.cloud_notm}} console](https://cloud.ibm.com/){: external} menu ![Menu icon](../icons/icon_hamburger.svg "Menu icon"), click **Containers** > **Clusters**.
3. From the **Clusters** page, click your cluster.
4. From the **Worker Nodes** tab, select the checkbox for each worker node that you want to update. An action bar is displayed over the table header row.
5. From the action bar, click **Update**.

If you have Portworx installed in your cluster, you must restart the Portworx pods on the updated worker nodes. For more information, see [Portworx limitations](/docs/openshift?topic=openshift-storage_portworx_plan#portworx_limitations).
{: important}

## Next steps
{: #classic-worker-next-steps}

Repeat the update process with other worker pools. When all worker pools are updated, [update your cluster components and managed add-ons](/docs/openshift?topic=openshift-update-components).

Notify all developers who work in the cluster to [update their `oc` CLI](/docs/openshift?topic=openshift-cli-install) to match the Kubernetes master version. Running a `oc` client that is two or more versions apart from the server version is not supported and can cause unexpected errors.
{: important}



## Related links
{: #classic-worker-related}

* [Updating clusters, worker nodes, and cluster components](/docs/openshift?topic=openshift-update)
* [Worker node states](/docs/openshift?topic=openshift-worker-node-state-reference)
* [After a worker node updates or reloads, why do duplicate nodes and pods appear?](/docs/openshift?topic=openshift-cs_duplicate_nodes)
