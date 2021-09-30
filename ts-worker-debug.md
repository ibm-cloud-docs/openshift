---

copyright: 
  years: 2014, 2021
lastupdated: "2021-09-30"

keywords: openshift, roks, rhoks, rhos

subcollection: openshift
content-type: troubleshoot

---




{{site.data.keyword.attribute-definition-list}}



# Debugging worker nodes
{: #debug_worker_nodes}
{: troubleshoot}
{: support}

Review the options to debug your worker nodes and find the root causes for failures.
{: shortdesc}

**Infrastructure provider**:
* <img src="images/icon-classic.png" alt="Classic infrastructure provider icon" width="15" style="width:15px; border-style: none"/> Classic
* <img src="images/icon-vpc.png" alt="VPC infrastructure provider icon" width="15" style="width:15px; border-style: none"/> VPC

## Step 1: Get the worker node state
{: #worker-debug-get-state}

If your cluster is in a **Critical**, **Delete failed**, or **Warning** state, or is stuck in the **Pending** state for a long time, review the state of your worker nodes.

```sh
ibmcloud oc worker ls --cluster <cluster_name_or_id>
```
{: pre}

## Step 2: Review the worker node state
{: #worker-debug-rev-state}

Review the **State** and **Status** field for every worker node in your CLI output.

For more information, see [Worker node states](/docs/openshift?topic=openshift-worker-node-state-reference).

## Step 3: Get the details for each worker node
{: #worker-debug-get-details}

Get the details for the worker node. If the details include an error message, review the list of [common error messages for worker nodes](/docs/containers?topic=containers-common_worker_nodes_issues) to learn how to resolve the problem.

```sh
ibmcloud oc worker get --cluster <cluster_name_or_id> --worker <worker_node_id>
```
{: pre}

## Step 4: Review the infrastructure provider for the worker node
{: #worker-debug-rev-infra}

Review the infrastructure environment to check for other reasons that might cause the worker node issues.
1. Check with your networking team to make sure that no recent maintenance, such as firewall or subnet updates, might impact the worker node connections.
2. Review [{{site.data.keyword.cloud_notm}}](https://cloud.ibm.com/status/){: external} for **{{site.data.keyword.openshiftlong_notm}}** and the underlying infrastructure provider, such as **Virtual Servers** for classic, **VPC** related components, or **{{site.data.keyword.satelliteshort}}**.
3. If you have access to the underlying infrastructure, such as classic **Virtual Servers**, review the details of the corresponding machines for the worker nodes.




