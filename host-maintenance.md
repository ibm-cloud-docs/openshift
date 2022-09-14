---

copyright:
  years: 2022, 2022
lastupdated: "2022-09-14"

keywords: maintenance, host maintenance, notification, workers, offline

subcollection: openshift

---

{{site.data.keyword.attribute-definition-list}}

# Preparing for host maintenance updates
{: #host-maintenance}

{{site.data.keyword.IBM_notm}} engineers perform host maintenance to improve stability, provide security enhancements, and support upcoming new features. At times, {{site.data.keyword.cloud_notm}} infrastructure providers perform maintenance on the hosts that house the Virtual Servers that are used as workers in your cluster, which may cause some of your workers to briefly go offline. However, there are actions you can take before the maintenance period that can minimize disruptions to your worker nodes. A notification with maintenance details and a list of affected workers is sent to customers prior to the maintenance window. Follow these steps to prepare your workers for an upcoming maintenance period.
{: shortdesc}

## Identifying your affected workers
{: #worker-maintenance-list}

If your workers are scheduled to undergo maintenance, you recieve a notification before the maintenance window begins. A list of the workers that are affected is included in the notification. 
{: shortdesc}

The list of impacted components may look similar to the following example. The steps documented here apply to the workers listed in the **IBM Kubernetes Service or RedHat OpenShift on IBM Cloud Workers** section.

```sh
**Virtual Server Instances scheduled for maintenance**

    Virtual Server Instances in your account:

           ID                                           Name
           1111_1a111aaa-1a1a-1aa1-1111-a11a111a1111    my_vpc_cluster_1

    Virtual Server Instances in service accounts:

        Application Load Balancer
            alb-11aa111a-1111111
    
        IBM Kubernetes Service or RedHat OpenShift on IBM Cloud workers
            kube-aaaa1aaa111aa11aa11a-aaaaaaaaaaa-aaaaaaa-00001a11
            kube-aaaa2aaa222aa22aa22a-aaaaaaaaaaa-aaaaaaa-00002a22
            kube-aaaa3aaa333aa33aa33a-aaaaaaaaaaa-aaaaaaa-00003a33

```
{: screen}


## Actions to take before the maintenance period
{: #worker-maintenance-actions}

Follow these steps to prepare your workers for the maintenance period. Workers can't be scheduled on hosts that are scheduled for maintenance. You can avoid disruptions to your workload by rebooting or replacing your workers so that they move to different hosts that are not undergoing maintenance. 
{: shortdesc}

### Workers in Classic clusters 
{: #worker-maintenance-classic}

For workers in Classic clusters, reboot the affected workers by following the steps for the [`ibmcloud oc worker reboot` command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reboot) in the CLI reference.
{: shortdesc}

### Workers in VPC clusters
{: #worker-maintenance-vpc}

For workers in VPC clusters, the steps to take depend on the flavor of the worker node. To check a worker node's flavor, run `ibmcloud oc worker get --worker <worker_id> --cluster <cluster_name_or_id>`.
{: shortdesc}

For workers with the `cx2.`, `bx2.`, or `mx2.` flavors
:   Reboot the affected workers by following the steps for the [`ibmcloud oc worker reboot` command](/docs/openshift?topic=openshift-kubernetes-service-cli#cs_worker_reboot) in the CLI reference.

For workers with the `cx2d.`, `bx2d.`, or `mx2d.` flavors
:   Complete the following steps

    1. Cordon and drain the worker.

        ```sh
        oc drain <worker_id>
        ```
        {: pre}

    2. Replace the worker node. For more information on replacing a worker node, see the [CLI reference](/docs/openshift?topic=openshift-kubernetes-service-cli#cli_worker_replace). 

        ```sh
        ibmcloud oc worker replace --cluster <cluster_name_or_ID> --worker <worker_node_ID>
        ```
        {: pre}

    3. Uncordon the worker.

        ```sh
        oc uncordon <worker_id>
        ```
        {: pre}
