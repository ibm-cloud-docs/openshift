---

copyright: 
  years: 2022, 2023
lastupdated: "2023-03-22"

keywords: flow logs, VPC monitoring, worker nodes, VPC, network traffic, collector

subcollection: openshift


---

{{site.data.keyword.attribute-definition-list}}




# Enabling Flow Logs for VPC cluster components
{: #vpc-flow-log}

You can configure {{site.data.keyword.cloud_notm}} {{site.data.keyword.fl_full}} to gather information about the traffic entering or leaving your VPC cluster worker nodes. Flow logs are stored in an {{site.data.keyword.cos_full_notm}} instance and can be used for troubleshooting purposes, adhering to compliance regulations, and more. For more information about {{site.data.keyword.fl_full}}, see [Flow logs use cases](/docs/vpc?topic=vpc-flow-logs&interface=ui#flow-logs-use-cases).
{: shortdesc}

When you use {{site.data.keyword.fl_full}} with a {{site.data.keyword.redhat_openshift_notm}} VPC cluster, you can enable flow logs at the VPC level, or at the VPC subnet or VPC load balancer level. You cannot specify which worker nodes to gather flow logs for. However, you can review the flow log output to identify information that is specific to the worker nodes you want to investigate.

## Configuring a flow log collector
{: #vpc-flow-log_create}

To configure flow logs at the VPC, VPC subnet, or VPC load balancer level, see [Creating a flow log collector](/docs/vpc?topic=vpc-ordering-flow-log-collector) in the VPC documentation. 
{: shortdesc}

To enable flow logs, you must have an {{site.data.keyword.cos_full_notm}} instance with a single-region bucket that is in the same region as the VPC resource you are monitoring. 
{: note}

## Viewing worker node flow logs
{: #vpc-flow-log_view}

Your {{site.data.keyword.fl_full}} gathers information from the VPC, VPC subnet, or VPC load balancer level. However, you can use the flow logs to gather information that is specific to your worker nodes. Separate flow log files are created for ingress and egress traffic. 
{: shortdesc}

1. In the CLI, find the `ibm-cloud.kubernetes.io/instance-id` label value for the worker node. 
    ```sh
    oc describe node <worker_node_ip> | grep instance-id
    ```
    Example output.
    ```sh
    ibm-cloud.kubernetes.io/instance-id=1010_a1aa1010-a1a0-1010-a1aa-aa1a1-a1-aa1
    ```
    {: screen}
    
2. In the {{site.data.keyword.cloud_notm}} UI, click your {{site.data.keyword.cos_full_notm}} instance in the **Resource list**.
3. Click the bucket where your flow logs are collected.
4. Download and decompress the flow log object. 
5. Open the file and navigate through the file directory until you reach directories that begin with `instance-id=`. 
6. Find the file directory that contains the instance ID found in the first step. The ID is included at the end of the file directory name.
    Example.
    ```sh
    `instance-id=crn%3AV1%...%3Ainstance%3A1010_a1aa1010-a1a0-1010-a1aa-aa1a1-a1-aa1
    ```
    {: screen}

6. In the `instance=id=` directory, locate the `record-type=ingress` and `record-type=egress` files. Your ingress and egress traffic logs are located here. 

