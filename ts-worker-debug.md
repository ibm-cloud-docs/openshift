---

copyright: 
  years: 2014, 2025
lastupdated: "2025-05-29"


keywords: openshift, kubernetes, help, network, connectivity, {{site.data.keyword.openshiftlong_notm}}

subcollection: openshift

content-type: troubleshoot

---

{{site.data.keyword.attribute-definition-list}}


# Debugging worker nodes
{: #debug_worker_nodes}
{: troubleshoot}
{: support}

[Virtual Private Cloud]{: tag-vpc} [Classic infrastructure]{: tag-classic-inf}

Review the options to debug your worker nodes and find the root causes for failures.
{: shortdesc}


## Check worker node notifications and maintenance updates
{: #worker-debug-notifs}

Check the {{site.data.keyword.cloud_notm}} health and status dashboard for any notifications or maintenance updates that might be relevant to your worker nodes. These notifications or updates might help determine the cause of the worker node failures.

1. [Classic clusters]{: tag-classic-inf} Check the [health dashboard](https://cloud.ibm.com/gen1/infrastructure/health-dashboard){: external} for any {{site.data.keyword.cloud_notm}} emergency maintenance notifications that might affect classic worker nodes in your account. Depending on the nature of the maintenance notification, you might need to reboot or reload your worker nodes. 
1. Check the {{site.data.keyword.cloud_notm}} [status dashboard](https://cloud.ibm.com/status){: external} for any known problems that might affect your worker nodes or cluster. If any of the following components show an error status, that component might be the cause of your worker node disruptions. 
    - For all clusters, check the **Kubernetes Service** and **Container Registry** components.
    - For Red Hat OpenShift clusters, check the **Red Hat OpenShift on IBM Cloud** component.
    - For VPC clusters, check the **Virtual Private Cloud**, **Virtual Private Endpoint** and **Virtual Server for VPC** components.
    - For Classic clusters, check the **Classic Infrastructure Provisioning** and **Virtual Servers** components.


## Quick steps to resolve worker node issues
{: #worker-debug-quick}

If your worker node is not functioning as expected, you can follow these steps to update your cluster and command line tools or run diagnostic tests. If the issue persists, see [Debugging your worker node](#worker-debug-steps) for additional steps. 
{: shortdesc}

1. [Update your cluster and worker nodes to the latest version](/docs/openshift?topic=openshift-update#update).
2. [Update your command line tools](/docs/openshift?topic=openshift-cli-update).
3. [Run tests in the Diagnostics and Debug Tool add-on](/docs/openshift?topic=openshift-debug-tool). 


## Debugging your worker node
{: #worker-debug-steps}

### Step 1: Get the worker node state
{: #worker-debug-get-state}

If your cluster is in a **Critical**, **Delete failed**, or **Warning** state, or is stuck in the **Pending** state for a long time, review the state of your worker nodes.

```sh
ibmcloud oc worker ls --cluster <cluster_name_or_id>
```
{: pre}

### Step 2: Review the worker node state
{: #worker-debug-rev-state}

Review the **State** and **Status** field for every worker node in your CLI output.

For more information, see [Worker node states](/docs/openshift?topic=openshift-worker-node-state-reference).

### Step 3: Get the details for each worker node
{: #worker-debug-get-details}

Get the details for the worker node. If the details include an error message, review the list of [common error messages for worker nodes](/docs/openshift?topic=openshift-common_worker_nodes_issues) to learn how to resolve the problem.

```sh
ibmcloud oc worker get --cluster <cluster_name_or_id> --worker <worker_node_id>
```
{: pre}

### Step 4: Review the infrastructure provider for the worker node
{: #worker-debug-rev-infra}

Review the infrastructure environment to check for other reasons that might cause the worker node issues.
1. Check with your networking team to make sure that no recent maintenance, such as firewall or subnet updates, might impact the worker node connections.
2. Review [{{site.data.keyword.cloud_notm}}](https://cloud.ibm.com/status/){: external} for **{{site.data.keyword.openshiftlong_notm}}** and the underlying infrastructure provider, such as **Virtual Servers** for classic, **VPC** related components, or **{{site.data.keyword.satelliteshort}}**.
3. If you have access to the underlying infrastructure, such as classic **Virtual Servers**, review the details of the corresponding machines for the worker nodes.




### Step 5: Gather the logs and other details about your worker nodes
{: #worker-debug-must-gather}

The `oc adm must-gather` CLI command collects the information from your cluster for debugging issues. The must-gather tool collects resource definitions, service logs, and more. Note that audit logs are not collected as part of the default set of information to reduce the size of the files.

When you run `oc adm must-gather`, a new pod with a random name is created in a new project on the cluster. The data is collected on that pod and saved in a new directory that starts with `must-gather.local`.

Review the following example commands.

```sh
oc adm must-gather
```
{: pre}

Example command to collect data related to one or more specific features, use the `--image` argument with a specific image.

```sh
oc adm must-gather \
--image=registry.redhat.io/container-native-virtualization/cnv-must-gather-rhel9:v4.17.5
```
{: pre}

Example command to collect audit logs.

```sh
oc adm must-gather -- /usr/bin/gather_audit_logs
```
{: pre}


Example command to run must-gather in a specific namespace.
```sh
oc adm must-gather --run-namespace <namespace> \
--image=registry.redhat.io/container-native-virtualization/cnv-must-gather-rhel9:v4.17.5
```
{: pre}

Example commands to collect the logs from a given timeframe.

```sh
oc adm must-gather --since=24h
```
{: pre}

```sh
oc adm must-gather --since-time=$(date -d '-24 hours' +%Y-%m-%dT%T.%9N%:z )
```
{: pre}

Example command to collect network logs.

```sh
oc adm must-gather -- gather_network_logs
```
{: pre}

For more examples and arguments run the following comamnd

```sh
oc adm must-gather -h
```
{: pre}

Example command to create a compressed file from the must-gather directory.
```sh
tar cvaf must-gather.tar.gz must-gather.local.5421342344627712289/
```
{: pre}

Attach the compressed file to your support case on of the [Red Hat Customer Portal](https://access.redhat.com/support/cases/#/case/list){: external}.
