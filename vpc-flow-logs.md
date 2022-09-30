---

copyright: 
  years: 2022, 2022
lastupdated: "2022-09-30"

keywords: flow logs, VPC monitoring, worker nodes, VPC, network traffic, collector

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}


# Enabling Flow Logs for VPC cluster components
{: #vpc-flow-log}

You can configure {{site.data.keyword.cloud_notm}} {{site.data.keyword.fl_full}} to gather information about the traffic entering or leaving your VPC cluster worker nodes. Flow logs are stored in a {{site.data.keyword.cos_full_notm}} instance and can be used for troubleshooting purposes, adhering to compliance regulations, and more. For more information about {{site.data.keyword.fl_full}}, see [Flow logs use cases](/docs/vpc?topic=vpc-flow-logs&interface=ui#flow-logs-use-cases).
{: shortdesc}

When you use {{site.data.keyword.fl_full}} with a {{site.data.keyword.redhat_openshift_notm}} VPC cluster, you can enable flow logs at the VPC level, or at the VPC subnet or VPC load balancer level. You cannot specify which worker nodes to gather flow logs for. However, you can review the flow log output to identify information that is specific to the worker nodes you want to investigate.

## Configuring a flow log collector
{: #vpc-flow-log_create}

To configure flow logs at the VPC, VPC subnet, or VPC load balancer level, see [Creating a flow log collector](/docs/vpc?topic=vpc-ordering-flow-log-collector) in the VPC documentation. 
{: shortdesc}

To enable flow logs, you must have a {{site.data.keyword.cos_full_notm}} instance with a single-region bucket that is in the same region as the VPC resource you are monitoring. 
{: note}

## Viewing worker node flow logs
{: #vpc-flow-log_view}

Your {{site.data.keyword.fl_full}} gathers information from the VPC, VPC subnet, or VPC load balancer level. However, you can use the flow logs to gather information that is specific to your worker nodes. Separate flow log files are created for egress and ingress traffic. 
{: shortdesc}

1. List your worker nodes and note the ID of the worker node you want to view.

    ```sh
    ibmcloud oc worker ls --cluster <cluster_name_or_id>
    ```
    {: pre}

2. In the {{site.data.keyword.cloud_notm}} UI, click your {{site.data.keyword.cos_full_notm}} instance in the **Resource list**.
3. Click the bucket that you specified when you created the flow log collector.
4. Download and uncompress the flow log object. 
5. Re-save the file as a `json` file.
6. Open the file. 
7. To find the entry that corresponds to a worker node, find the `instance_crn` value that matches the ID of the worker node you found previously.
